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

Expected output
<pre>
(jegan@tektutor.org)$ oc new-app --name hello https://github.com/tektutor/openshift-aug-2022.git#main --context-dir=Day5/spring-ms-multistage --strategy=docker
--> Found container image 0c30846 (2 weeks old) from registry.redhat.io for "registry.redhat.io/ubi8/openjdk-11:latest"

    Java Applications 
    ----------------- 
    Platform for building and running plain Java applications (fat-jar and flat classpath)

    Tags: builder, java

    * An image stream tag will be created as "openjdk-11:latest" that will track the source image
    * A Docker build using source code from https://github.com/tektutor/openshift-aug-2022.git#main will be created
      * The resulting image will be pushed to image stream tag "hello:latest"
      * Every time "openjdk-11:latest" changes a new build will be triggered

--> Creating resources ...
    imagestream.image.openshift.io "hello" created
    buildconfig.build.openshift.io "hello" created
    deployment.apps "hello" created
    service "hello" created
--> Success
    Build scheduled, use 'oc logs -f buildconfig/hello' to track its progress.
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/hello' 
    Run 'oc status' to view your app.
</pre>


### Checking build logs
```
oc logs -f bc/hello
```
