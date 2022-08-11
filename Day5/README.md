# Day 5

## Deploying an application using Dockerfile from Github repo in a sub-folder
```
oc new-project jegan
oc new-app --name hello https://github.com/tektutor/openshift-aug-2022.git --context-dir=Day2/spring-ms
oc expose svc/hello
```

## Deploying an application using plain source code with Image suggestion
```
oc project jegan
oc new-app --name hello registry.redhat.io/ubi8/openjdk-11:latest~https://github.com/tektutor/openshift-aug-2022.git#main --context-dir=Day5/spring-ms
oc expose svc/hello
```

## Deploying an application using multi-stage Dockerfile from GitHub repo
```
oc project jegan
oc new-app --name hello https://github.com/tektutor/openshift-aug-2022.git#main --context-dir=Day5/spring-ms-multistage --strategy=docker
oc expose svc/hello
```
