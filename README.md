## Udacity Microservices at Scale using AWS & Kubernetes ##
## Deployt EKS Using CloudFormation
- Source config on folder kubernetes/eks.yaml
- Source parameters on folder kubernetes/server-parameters.json

## My github link

- https://github.com/phan-van-thuy/codebuild

# Udacity Microservices at Scale using AWS & Kubernetes

In this project, we will apply our skills to build an application that connects to the Postgres database. Including:

* Works on AWS
* Use ECR to store the latest version application images
* Use Codebuild to deploy image storage to ECR automatically
* Work with CloudFormation to deploy Kubernetes infrastructure
* Use helm to deploy Postgres database
* Build a Kubernetes cluster and deploy microservices

## Environment Variables

To run this project, you will need to add the following environment variables to your CircleCI environment variables

* `AWS_DEFAULT_REGION`
* `AWS_ACCOUNT_ID`
* `IMAGE_APP_REPO_NAME`
* `IMAGE_APP_TAG`
* `IMAGE_DB_REPO_NAME`
* `IMAGE_DB_TAG`

## Folder structure

| File | Description |
| ---- | ----------- |
| `application/Dockerfile` | Build image application |
| `codebuild` | the job automatically pushes images to ECR |
| `codebuild/buildspec.yml` | template codebuild |
| `db` | Database for postgre |
| `deployment` | Kubernetes resource files deployment |
| `deployment/configmap.yaml` | file configmap for username, host, port connect from application to postgres |
| `deployment/deployment.yaml` | File config deploy application |
| `deployment/provisioner.yaml` | File config deploy CSI Drive for PV, PVC postgres |
| `deployment/secret.yaml` | File config password for postgesql |
| `deployment/services.yaml` | File config servive for application |
| `kubernetes` | Folder for deploy kubernetes infra using cloudformation |
| `kubernetes/eks.yaml` | File config template cloudformation |
| `screenshot` | Folder screenshot project |

## Build Cluster kubernetes
## Deploy cluster kubernetes using cloudformation
* Run `aws cloudformation deploy --template-file eks.yml --stack-name eks  --tags project=udapeople --capabilities CAPABILITY_NAMED_IAM` to create EKS cluster

* Some kubectl commands to check k8s resources
    # Fet k8s configs
    aws eks --region us-east-1 update-kubeconfig --name eks
    # check all deployment
    kubectl get all

## Build Postgresql
* Run helm repo add database https://charts.bitnami.com/bitnami
* helm install postgres database/postgresql
## Deploy application to Kubernetes
* Run kubectl apply -f /deployment
* Show all pod, svc, deployment run 
    kubectl get all