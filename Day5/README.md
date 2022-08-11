# Day 5

## Deploying an application using Dockerfile from Github repo in a sub-folder
```
oc new-project jegan
oc new-app --name hello https://github.com/tektutor/openshift-aug-2022.git --context-dir=Day2/spring-ms
oc expose svc/hello
```

