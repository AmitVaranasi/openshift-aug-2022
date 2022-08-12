# Day 5

## ⛹️‍♀️ Lab - Deploying an application using Dockerfile from Github repo in a sub-folder
```
oc new-project jegan
oc new-app --name hello https://github.com/tektutor/openshift-aug-2022.git --context-dir=Day2/spring-ms
oc expose svc/hello
```

## ⛹️‍♀️ Lab -  Deploying an application using plain source code with Image suggestion
```
oc project jegan
oc new-app --name hello registry.redhat.io/ubi8/openjdk-11:latest~https://github.com/tektutor/openshift-aug-2022.git#main --context-dir=Day5/spring-ms
oc expose svc/hello
```

## ⛹️‍♂️ Lab - Deploying an application using multi-stage Dockerfile from GitHub repo
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


### Check build logs and create a route
```
oc logs -f bc/hello
oc get svc
oc expose svc/hello
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc get svc</b>
NAME    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
hello   ClusterIP   172.30.192.195   <none>        8080/TCP,8443/TCP,8778/TCP   5m15s
(jegan@tektutor.org)$ <b>oc expose svc/hello</b>
route.route.openshift.io/hello exposed
</pre>

## ⛹️‍♀️ Lab - Creating a Building with an docker image output

Let's first create the ImageStream resource
```
cd ~/openshift-aug-2022
git pull

cd Day5/ImageStreamAndBuildConfig
oc apply -f imagestream.yml 
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc apply -f imagestream.yml</b>
imagestream.image.openshift.io/tektutor-spring-hello created
</pre>

Listing the imagestream
```
(jegan@tektutor.org)$ <b>oc get is</b>
NAME                    IMAGE REPOSITORY                                                               TAGS   UPDATED
tektutor-spring-hello   image-registry.openshift-image-registry.svc:5000/jegan/tektutor-spring-hello 
```

Let's create the buildconfig and start the build
```
cd ~/openshift-aug-2022
git pull

cd Day5/ImageStreamAndBuildConfig
oc apply -f buildconfig.yml
```

Expected output
<pre>
(jegan@tektutor.org)$ oc apply -f buildconfig.yml 
buildconfig.build.openshift.io/spring-hello created
</pre>

Listing the build config
```
oc get bc
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc get bc</b>
NAME           TYPE     FROM   LATEST
spring-hello   Docker   Git    1
</pre>

Checking the build output
```
oc logs -f bc/spring-hello
```

## ⛹️‍♀️ Lab - Deleting an image from OpenShift container registry
```
oc get images| grep image-registry.openshift-image-registry.svc:5000 | grep tektutor-spring-hello

oc delete image sha256:22f454e8a66f899723017653de4e2d182ef0142ba26ac60d472e48eae7dda58b
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc get images| grep image-registry.openshift-image-registry.svc:5000 | grep tektutor-spring-hello</b>
sha256:22f454e8a66f899723017653de4e2d182ef0142ba26ac60d472e48eae7dda58b   image-registry.openshift-image-registry.svc:5000/jegan/tektutor-spring-hello@sha256:22f454e8a66f899723017653de4e2d182ef0142ba26ac60d472e48eae7dda58b

(jegan@tektutor.org)$ <b>oc delete image sha256:22f454e8a66f899723017653de4e2d182ef0142ba26ac60d472e48eae7dda58b</b>
image.image.openshift.io "sha256:22f454e8a66f899723017653de4e2d182ef0142ba26ac60d472e48eae7dda58b" deleted
</pre>
