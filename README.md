# helm-repo

####################### DEPLOYMENT WITH HELM ###############################

Create a helm-repo directory
sysadmin@ubuntuminikube:~$ mkdir helm-repo

Create helm chart hello-app

sysadmin@ubuntuminikube:~$ cd helm-repo
sysadmin@ubuntuminikube:~/helm-repo$ helm create hello-app
Creating hello-app
sysadmin@ubuntuminikube:~/helm-repo$ ls
hello-app
sysadmin@ubuntuminikube:~/helm-repo$ cd hello-app
sysadmin@ubuntuminikube:~/helm-repo/hello-app$ ls
charts  Chart.yaml  templates  values.yaml
sysadmin@ubuntuminikube:~/helm-repo/hello-app$ cd templates
sysadmin@ubuntuminikube:~/helm-repo/hello-app/templates$ ls
deployment.yaml  _helpers.tpl  hpa.yaml  ingress.yaml  NOTES.txt  serviceaccount.yaml  service.yaml  tests

Edit the helm files with the configuration parameters, the values file contains the main configuration parameters
Package the hello-app with helm

sysadmin@ubuntuminikube:~$ cd helm-repo
sysadmin@ubuntuminikube:~/helm-repo$ helm package hello-app
Successfully packaged chart and saved it to: /home/sysadmin/helm-repo/hello-app-0.1.0.tgz

Install the helm release with the package

sysadmin@ubuntuminikube:~/helm-repo$ helm install hello-app ./hello-app-0.1.0.tgz
NAME: hello-app
LAST DEPLOYED: Tue Oct 19 03:35:10 2021
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=hello-app,app.kubernetes.io/instance=hello-app" -o jsonpath="{.items[0].metadata.name}")
  export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT

sysadmin@ubuntuminikube:~/helm-repo$ helm list
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
hello-app       default         1               2021-10-19 03:35:10.901360953 +0000 UTC deployed        hello-app-0.1.0 1.16.0


################### PUSHING HELM-REPO REPOSITORY TO GIT #########################

sysadmin@ubuntuminikube:~$ cd helm-repo
sysadmin@ubuntuminikube:~/helm-repo$ git init
Initialized empty Git repository in /home/sysadmin/helm-repo/.git/
sysadmin@ubuntuminikube:~/helm-repo$ git config --global user.email tosyn126@yahoo.com
sysadmin@ubuntuminikube:~/helm-repo$ git config --global user.name Oluolapeju
sysadmin@ubuntuminikube:~/helm-repo$ git add "/home/sysadmin/helm-repo/"
sysadmin@ubuntuminikube:~/helm-repo$  git commit -m "first commit"
[master (root-commit) 558445d] first commit
 12 files changed, 405 insertions(+)
 create mode 100644 hello-app-0.1.0.tgz
 create mode 100644 hello-app/.helmignore
  create mode 100644 hello-app/Chart.yaml
 create mode 100644 hello-app/templates/NOTES.txt
 create mode 100644 hello-app/templates/_helpers.tpl
 create mode 100644 hello-app/templates/deployment.yaml
 create mode 100644 hello-app/templates/hpa.yaml
 create mode 100644 hello-app/templates/ingress.yaml
 create mode 100644 hello-app/templates/service.yaml
 create mode 100644 hello-app/templates/serviceaccount.yaml
 create mode 100644 hello-app/templates/tests/test-connection.yaml
 create mode 100644 hello-app/values.yaml
sysadmin@ubuntuminikube:~/helm-repo$ git branch -M main
sysadmin@ubuntuminikube:~/helm-repo$ git remote add master https://github.com/Oluolapeju/helm-repo.git
sysadmin@ubuntuminikube:~/helm-repo$ git push -u master main
Enumerating objects: 17, done.
Counting objects: 100% (17/17), done.
Delta compression using up to 6 threads
Compressing objects: 100% (16/16), done.
Writing objects: 100% (17/17), 9.28 KiB | 9.28 MiB/s, done.
Total 17 (delta 0), reused 0 (delta 0)
To https://github.com/Oluolapeju/helm-repo.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'master'.
sysadmin@ubuntuminikube:~/helm-repo$
new task




