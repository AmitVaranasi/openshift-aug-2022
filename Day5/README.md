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

Expected output (Only the last few lines are pasted here)
<pre>
30076a5355466d822b2e3466d9a4c3910ecc"
--> 700719db884
[2/2] STEP 5/5: LABEL "io.openshift.build.commit.author"="Jeganathan Swaminathan <mail2jegan@gmail.com>" "io.openshift.build.commit.date"="Fri Aug 12 06:40:48 2022 +0530" "io.openshift.build.commit.id"="5a2a30076a5355466d822b2e3466d9a4c3910ecc" "io.openshift.build.commit.message"="Update README.md" "io.openshift.build.commit.ref"="main" "io.openshift.build.name"="spring-hello-1" "io.openshift.build.namespace"="jegan" "io.openshift.build.source-context-dir"="Day5/ImageStreamAndBuildConfig" "io.openshift.build.source-location"="https://github.com/tektutor/openshift-aug-2022.git"
[2/2] COMMIT temp.builder.openshift.io/jegan/spring-hello-1:81ec71e7
--> f447bd29660
Successfully tagged temp.builder.openshift.io/jegan/spring-hello-1:81ec71e7
f447bd29660c4b70800af1dc1adc056a5a2073f4896f0ee963ad21bc539c23ed

Pushing image image-registry.openshift-image-registry.svc:5000/jegan/tektutor-spring-hello:latest ...
Getting image source signatures
Copying blob sha256:1e09a5ee0038fbe06a18e7f355188bbabc387467144abcd435f7544fef395aa1
Copying blob sha256:0d725b91398ed3db11249808d89e688e62e511bbd4a2e875ed8493ce1febdb2c
Copying blob sha256:e441d34134fac91baa79be3e2bb8fb3dba71ba5c1ea012cb5daeb7180a054687
Copying blob sha256:dab0c9d1d83f19939b2d1c95969e68abd9ba8b4e0f2b6c4866e3355393b4a2ca
Copying config sha256:f447bd29660c4b70800af1dc1adc056a5a2073f4896f0ee963ad21bc539c23ed
Writing manifest to image destination
Storing signatures
Successfully pushed image-registry.openshift-image-registry.svc:5000/jegan/tektutor-spring-hello@sha256:faecafdf6485c222df0b56e97cce4a36cd843f3473f91d987303b58b785ba9ce
Push successful
</pre>


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

## ⛹️‍♂️ Lab - Deploying a Python Django application using Template file
```
cd ~/openshift-aug-2022
git pull

cd Day5/templates/django-ex
oc create -f openshift/templates/django-postgresql.json
```

Expected output
<pre>
(jegan@tektutor.org)$ git clone https://github.com/sclorg/django-ex.git
Cloning into 'django-ex'...
remote: Enumerating objects: 1040, done.
remote: Counting objects: 100% (18/18), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 1040 (delta 4), reused 10 (delta 2), pack-reused 1022
Receiving objects: 100% (1040/1040), 299.57 KiB | 524.00 KiB/s, done.
Resolving deltas: 100% (460/460), done.
(jegan@tektutor.org)$ ls
django-ex
(jegan@tektutor.org)$ <b>cd django-ex</b>
(jegan@tektutor.org)$ <b>ls</b>
conf  manage.py  openshift  project  README.md  requirements.txt  welcome  wsgi.py
(jegan@tektutor.org)$ ls openshift/templates/
django.json  django-postgresql.json  django-postgresql-persistent.json
(jegan@tektutor.org)$ ls
conf  manage.py  openshift  project  README.md  requirements.txt  welcome  wsgi.py
(jegan@tektutor.org)$ <b>oc create -f openshift/templates/django-postgresql.json</b>
W0812 07:09:19.684047   34200 shim_kubectl.go:58] Using non-groupfied API resources is deprecated and will be removed in a future release, update apiVersion to "template.openshift.io/v1" for your resource
template.template.openshift.io/django-psql-example created
</pre>

The above steps will create the template within the OpenShift but won't deploy the application yet.
Let's list the templates installed in your OpenShift cluster under your project.

```
oc get templates
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc get templates</b>
NAME                  DESCRIPTION                                                                        PARAMETERS     OBJECTS
django-psql-example   An example Django application with a PostgreSQL database. For more informatio...   19 (5 blank)   8
</pre>

Let's deploy the application using the above template.
```
oc new-app django-psql-example
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc new-app django-psql-example</b>
--> Deploying template "jegan/django-psql-example" to project jegan

     Django + PostgreSQL (Ephemeral)
     ---------
     An example Django application with a PostgreSQL database. For more information about using this template, including OpenShift considerations, see https://github.com/sclorg/django-ex/blob/master/README.md.
     
     WARNING: Any data stored will be lost upon pod destruction. Only use this template for testing.

     The following service(s) have been created in your project: django-psql-example, postgresql.
     
     For more information about using this template, including OpenShift considerations, see https://github.com/sclorg/django-ex/blob/master/README.md.

     * With parameters:
        * Name=django-psql-example
        * Namespace=openshift
        * Version of Python Image=3.8-ubi8
        * Version of PostgreSQL Image=12-el8
        * Memory Limit=512Mi
        * Memory Limit (PostgreSQL)=512Mi
        * Git Repository URL=https://github.com/sclorg/django-ex.git
        * Git Reference=
        * Context Directory=
        * Application Hostname=
        * GitHub Webhook Secret=sdiofyNeMsaKKpfXy5y5tNWUTWQcsGIy5HoXbsSp # generated
        * Database Service Name=postgresql
        * Database Engine=postgresql
        * Database Name=default
        * Database Username=django
        * Database User Password=cqEGUaEu7qkPJWr7 # generated
        * Application Configuration File Path=
        * Django Secret Key=n5q7DR1XhYxfdABp5qCUa9f9XI5gH1DgjZiRMdH0PpZ5f9gzMm # generated
        * Custom PyPi Index URL=

--> Creating resources ...
    secret "django-psql-example" created
    service "django-psql-example" created
    route.route.openshift.io "django-psql-example" created
    imagestream.image.openshift.io "django-psql-example" created
    buildconfig.build.openshift.io "django-psql-example" created
    deploymentconfig.apps.openshift.io "django-psql-example" created
    service "postgresql" created
    deploymentconfig.apps.openshift.io "postgresql" created
--> Success
    Access your application via route 'django-psql-example-jegan.apps.ocp.tektutor.org' 
    Build scheduled, use 'oc logs -f buildconfig/django-psql-example' to track its progress.
    Run 'oc status' to view your app.
</pre>

List the build config
```
oc get bc
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc get bc</b>
NAME                  TYPE     FROM   LATEST
<b>django-psql-example   Source   Git    1</b>
spring-hello          Docker   Git    1
</pre>

Check the build logs
```
oc logs -f bc/django-psql-example
```

Expected output ( Only the last few lines are shown below )
<pre>
----------------------------------------------------------------------
Ran 3 tests in 0.055s

OK
Destroying test database for alias 'default'...
[3/3] STEP 1/1: FROM 048f290a28d7df18e4d1c359d0c37c279838244e922cf31407d019cbc9df3897
[3/3] COMMIT temp.builder.openshift.io/jegan/django-psql-example-1:dfe3dbf6
--> 048f290a28d
Successfully tagged temp.builder.openshift.io/jegan/django-psql-example-1:dfe3dbf6
048f290a28d7df18e4d1c359d0c37c279838244e922cf31407d019cbc9df3897

Pushing image image-registry.openshift-image-registry.svc:5000/jegan/django-psql-example:latest ...
Getting image source signatures
Copying blob sha256:c33176e339ee0c3bc814252724e1957c06414c2e695d2f14771fb44349e73cdb
Copying blob sha256:354c079828fae509c4f8e4ccb59199d275f17b0f26b1d7223fd64733788edf32
Copying blob sha256:e0dc1b5a4801cf6fec23830d5fcea4b3fac076b9680999c49935e5b50a17e63b
Copying blob sha256:471b87de02e1ccb2e2372afc08241872c651c1cc6444e888b966893b30d6d166
Copying blob sha256:7e3624512448126fd29504b9af9bc034538918c54f0988fb08c03ff7a3a9a4cb
Copying blob sha256:db0f4cd412505c5cc2f31cf3c65db80f84d8656c4bfa9ef627a6f532c0459fc4
Copying config sha256:048f290a28d7df18e4d1c359d0c37c279838244e922cf31407d019cbc9df3897
Writing manifest to image destination
Storing signatures
Successfully pushed image-registry.openshift-image-registry.svc:5000/jegan/django-psql-example@sha256:cc18d5a6cead748461119846024d62c4a4dec232830a1d1882300bbc497b7374
Push successful
</pre>

You should be able to access the Django Python web application that uses Postgres database from OpenShift webconsole.
