# Day 4

## ⛹️‍♂️ Lab - Pod port-forwarding for quick test
```
oc port-forward pod/nginx-78644964b4-xqp77 8080:8080
```

In the above command, 
 - port 8080 that appears on the left side is the port on the local machine.
 - port 8080 that appears on the right side is the container port where nginx server is listening

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc port-forward pod/nginx-78644964b4-xqp77 8080:8080</b>
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
Handling connection for 8080
</pre>

## ⛹️‍♂️ Lab - Demonstrates how a cloud native application can retrieve config details from Configmap
```
cd ~/openshift-aug-2022
git pull

cd Day3/configmap
oc apply -f software-tools-cm.yml
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc apply -f software-tools-cm.yml</b>
configmap/software-tools-cm created
</pre>

Let's create the pod that uses the configmap values
```
cd ~/openshift-aug-2022
git pull

cd Day3/configmap
oc apply -f my-pod.yml
```

Expected output
<pre>
(jegan@tektutor.org)$ oc apply -f my-pod.yml 
pod/my-pod created
</pre>

List and check if the my-pod is running
<pre>
(jegan@tektutor.org)$ oc get po
NAME                     READY   STATUS    RESTARTS   AGE
<b>my-pod                   1/1     Running   0          7s</b>
nginx-78644964b4-s5qgr   1/1     Running   0          47m
nginx-78644964b4-wdb2b   1/1     Running   0          47m
nginx-78644964b4-xqp77   1/1     Running   0          47m
</pre>

Verifying if the config map values are accessible within the pod
```
oc rsh pod/my-pod
echo $MAVEN_HOME
echo $JDK_HOME
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc rsh pod/my-pod</b>
$ ls
50x.html  index.html
$ <b>echo $MAVEN_HOME</b>
/usr/share/maven
$ echo $JDK_HOME
/usr/lib/jvm/jdk-11-jdk11
$ exit
</pre>

### See if you can access the web page from the Pod after port-forward in a different terminal
```
curl localhost:8080
```
Expected output
<pre>
(jegan@tektutor.org)$ <b>curl localhost:8080</b>
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
</pre>

## ⛹️‍♂️ Lab - Secret values in Kubernetes/OpenShift are base64 encoded values in data section
<pre>
(jegan@tektutor.org)$ <b>echo -n root|base64</b>
cm9vdA==
(jegan@tektutor.org)$ <b>echo -n Root@123|base64</b>
Um9vdEAxMjM=
</pre>

## Using Secrets to store mysql login credentials
```
cd ~/openshift-aug-2022
git pull

cd Day4/secret
oc apply -f mysql-login-credentials.yml
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc apply -f mysql-login-credentials.yml</b>
secret/mysql-login-credentials created
</pre>

### Listing the secrets
```
oc get secrets
```

Expected output
<pre>
(jegan@tektutor.org)$ oc get secrets
NAME                                 TYPE                                  DATA   AGE
builder-dockercfg-n279r              kubernetes.io/dockercfg               1      3h10m
builder-token-gbdvb                  kubernetes.io/service-account-token   4      3h10m
builder-token-njs2v                  kubernetes.io/service-account-token   4      3h10m
default-dockercfg-w7zp2              kubernetes.io/dockercfg               1      3h10m
default-token-kbdz7                  kubernetes.io/service-account-token   4      3h10m
default-token-ww7vr                  kubernetes.io/service-account-token   4      3h10m
deployer-dockercfg-9p684             kubernetes.io/dockercfg               1      3h10m
deployer-token-cfbzm                 kubernetes.io/service-account-token   4      3h10m
deployer-token-mbn2t                 kubernetes.io/service-account-token   4      3h10m
<b>mysql-login-credentials              Opaque                                2      3s</b>
</pre>

### See if you can print the value stores in the secrets using describe command
```
oc describe secret/mysql-login-credentials
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc describe secret/mysql-login-credentials</b>
Name:         mysql-login-credentials
Namespace:    jegan
Labels:       app=mysql
Annotations:  <none>

Type:  Opaque

Data
====
username:  4 bytes
password:  8 bytes
</pre>

## Removing existing label from a node
```
oc label node master-1.ocp.tektutor.org distype-
```
In the above command distype is the label key.

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc label node master-1.ocp.tektutor.org distype-</b>
node/master-1.ocp.tektutor.org unlabeled
</pre>


## ⛹️‍♀️ Lab - Understanding Nodeaffinity with mandatory scheduling rules

Initially let's ensure the label diskType=ssd doesn't exist in any node.
```
oc get nodes -l diskType=ssd
```
Expected output
<pre>
(jegan@tektutor.org)$ <b>oc get nodes -l diskType=ssd</b>
No resources found
</pre>

Let's deploy the pod in our openshift cluster now
```
cd ~/openshift-aug-2022
git pull

cd Day4/node-affinity-scheduling/
oc apply -f pod-with-mandatory-affinity-rules.yml
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc apply -f pod-with-mandatory-affinity-rules.yml</b>
pod/my-pod created
(jegan@tektutor.org)$ <b>oc get po -w</b>
NAME     READY   STATUS    RESTARTS   AGE
my-pod   0/1     <b>Pending</b>   0          4s
</pre>

As you can notice, the status is Pending.  This is because the scheduler wasn't able to find any node that has the label diskType=ssd.

Let's assign the label diskType=ssd to master-2 node
```
oc label node master-2.ocp.tektutor.org diskType=ssd
oc get nodes -l diskType=ssd
oc get po
```
Expected output
<pre>
(jegan@tektutor.org)$ <b>oc label node master-2.ocp.tektutor.org diskType=ssd</b>
node/master-2.ocp.tektutor.org labeled
(jegan@tektutor.org)$ <b>oc get nodes -l diskType=ssd</b>
NAME                        STATUS   ROLES           AGE    VERSION
master-2.ocp.tektutor.org   Ready    master,worker   2d4h   v1.23.5+012e945
(jegan@tektutor.org)$ <b>oc get po</b>
NAME     READY   STATUS    RESTARTS   AGE
my-pod   1/1     Running   0          3m7s
</pre>


## ⛹️‍♀️ Lab - Understanding Nodeaffinity with preferred(optional) scheduling preferences

Initially let's ensure the label diskType=ssd doesn't exist in any node.
```
oc get nodes -l diskType=ssd
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc get nodes -l diskType=ssd</b>
NAME                        STATUS   ROLES           AGE    VERSION
master-2.ocp.tektutor.org   Ready    master,worker   2d5h   v1.23.5+012e945
</pre>

Let's remove the label from the master-2 node
```
oc label node master-2.ocp.tektutor.org diskType-
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc label node master-2.ocp.tektutor.org diskType-</b>
node/master-2.ocp.tektutor.org unlabeled
</pre>

Let's deploy the pod in our openshift cluster now
```
cd ~/openshift-aug-2022
git pull

cd Day4/node-affinity-scheduling/
oc delete -f pod-with-mandatory-affinity-rules.yml
oc apply -f pod-with-preffered-affinity.yml
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc delete -f pod-with-mandatory-affinity-rules.yml</b>
pod "my-pod" deleted
(jegan@tektutor.org)$ <b>oc apply -f pod-with-preffered-affinity.yml</b>
pod/my-pod created
(jegan@tektutor.org)$ <b>oc get po -w</b>
NAME     READY   STATUS    RESTARTS   AGE
my-pod   1/1     Running   0          8s
</pre>


As you can notice, the status is Running.  The scheduler looks for nodes that has diskType=ssd label, if it finds a node that matches the criteria then the pod will be deployed there, otherwise Scheduler will deploy on some nodes ignoring the preferrence. 

## ⛹️‍♂️ Lab - Creating a CronJob that runs every 1 hour and prints hello
```
cd ~/openshift-aug-2022
git pull
cd Day4/cronjob

oc apply -f cronjob.yml
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc apply -f cronjob.yml</b>
cronjob.batch/hello created
</pre>

You can observe from the OpenShift webconsole, every 1 hour it spins a new Pod that print Hello and completes.  This goes on forever.


## Ingress
- Let's say you have multiple services for deployments
- If you wish to forward the traffic to different services depending on url path
- Forwarding rule

- assume my main url is tektutor.org
      tektutor.org/login  => login cluster-ip service
      tektutor.org/logout => logout node-port service
      tektutor.org/reports => reports load-balancer service

- For Ingress to work, we need IngressController and LoadBalancer
- OpenShift as part of installation it comes with HAProxy LoadBalancer
- Whenever we create a Ingress rule (Yaml of kind Ingress), the IngressController it will read the ingress rules
  that we wrote in the Ingress yaml file and then configures the HAProxy Load Balancer so that it can route the
  calls to different appropriate services.
  
## ⛹️‍♂️ Lab - Understanding Ingress rules

Let's deploy wordpress
```
cd ~/openshift-aug-2022
git pull
cd Day3/HELM

helm install wordpress-0.1.0.tgz
```

Let's deploy nginx
```
oc create deploy nginx --image=bitnami/nginx:latest  --replicas=3
oc expose deploy/nginx --port=8080
```

Now you can create the ingress. You need to edit ingress.yml and replace tektutor.org with rps.com in the host.
```
cd ~/openshift-aug-2022
git pull
cd Day4/ingress

oc apply -f ingress.yml
```

Listing the ingress
```
oc get ingress
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc get ingress</b>
NAME       CLASS    HOSTS                            ADDRESS                                PORTS   AGE
tektutor   <none>   tektutor.apps.ocp.tektutor.org   router-default.apps.ocp.tektutor.org   80      25m
</pre>


Testing the ingress
- Open your chrome browser on the lab machine
- type your ingress hostname e.g tektutor.apps.ocp.tektutor.org/wordpress
- type your ingress hostname e.g tektutor.apps.ocp.tektutor.org/nginx

You need to update the hostname as per your cluster domain and ingress name.

## ⛹️‍♀️ Lab - Securing your application routes

In my lab machine, the openshift self-signed certificate has expired. Hence, I had to create a new self-signed certifacte.

Generate CA files serverca.crt and serverkey.pem.  This allows signing the server and client keys.
```
openssl genrsa -out servercakey.pem
openssl req -new -x509 -key servercakey.pem -out serverca.crt
```

Expected output
<pre>
(jegan@tektutor.org)$ openssl genrsa -out servercakey.pem
Generating RSA private key, 2048 bit long modulus (2 primes)
..................................+++++
........................................................................+++++
e is 65537 (0x010001)

(jegan@tektutor.org)$ <b>openssl req -new -x509 -key servercakey.pem -out serverca.crt</b>
Can't load /home/jegan/.rnd into RNG
140631709282752:error:2406F079:random number generator:RAND_load_file:Cannot open file:../crypto/rand/randfile.c:88:Filename=/home/jegan/.rnd
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:IN
State or Province Name (full name) [Some-State]:Tamil Nadu
Locality Name (eg, city) []:Hosur
Organization Name (eg, company) [Internet Widgits Pty Ltd]:TekTutor
Organizational Unit Name (eg, section) []:Software
Common Name (e.g. server FQDN or YOUR name) []:ocp.tektutor.org
Email Address []:jegan@tektutor.org
</pre>

Let's create teh server private key(server.crt) and public key(server.key)
```
openssl genrsa -out server.key
openssl req -new -key server.key -out server_reqout.txt
openssl x509 -req -in server_reqout.txt -days 3650 -sha256 -CAcreateserial -CA serverca.crt -CAkey servercakey.pem -out server.crt
```

Expected output
<pre>
(jegan@tektutor.org)$ openssl genrsa -out server.key
Generating RSA private key, 2048 bit long modulus (2 primes)
.............................+++++
.....................................................+++++
e is 65537 (0x010001)
(jegan@tektutor.org)$ openssl req -new -key server.key -out server_reqout.txt
Can't load /home/jegan/.rnd into RNG
140071426494912:error:2406F079:random number generator:RAND_load_file:Cannot open file:../crypto/rand/randfile.c:88:Filename=/home/jegan/.rnd
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:IN
State or Province Name (full name) [Some-State]:Tamil Nadu
Locality Name (eg, city) []:Hosur
Organization Name (eg, company) [Internet Widgits Pty Ltd]:TekTutor
Organizational Unit Name (eg, section) []:Software
Common Name (e.g. server FQDN or YOUR name) []:ocp.tektutor.org
Email Address []:jegan@tektutor.org

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:root@123
An optional company name []:^C
(jegan@tektutor.org)$ openssl req -new -key server.key -out server_reqout.txt
Can't load /home/jegan/.rnd into RNG
140596477448640:error:2406F079:random number generator:RAND_load_file:Cannot open file:../crypto/rand/randfile.c:88:Filename=/home/jegan/.rnd
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:IN
State or Province Name (full name) [Some-State]:Tamil Nadu
Locality Name (eg, city) []:Hosur
Organization Name (eg, company) [Internet Widgits Pty Ltd]:TekTutor
Organizational Unit Name (eg, section) []:Software
Common Name (e.g. server FQDN or YOUR name) []:ocp.tektutor.org
Email Address []:jegan@tektutor.org

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
(jegan@tektutor.org)$ openssl x509 -req -in server_reqout.txt -days 3650 -sha256 -CAcreateserial -CA serverca.crt -CAkey servercakey.pem -out server.crt
Signature ok
subject=C = IN, ST = Tamil Nadu, L = Hosur, O = TekTutor, OU = Software, CN = ocp.tektutor.org, emailAddress = jegan@tektutor.org
Getting CA Private Key
</pre>

## Create the client private key(client.crt) and public key(client.key)
```
openssl genrsa -out client.key
openssl req -new -key client.key -out client_reqout.txt
openssl x509 -req -in client_reqout.txt -days 3650 -sha256 -CAcreateserial -CA  serverca.crt -CAkey servercakey.pem -out client.crt
```
When prompted for password, I type 'root@123' as the password for the passphrase.

Expected output
<pre>
(jegan@tektutor.org)$ openssl genrsa -out client.key
Generating RSA private key, 2048 bit long modulus (2 primes)
.......+++++
.........................................................................................................................+++++
e is 65537 (0x010001)
(jegan@tektutor.org)$ openssl req -new -key client.key -out client_reqout.txt
Can't load /home/jegan/.rnd into RNG
140654754931136:error:2406F079:random number generator:RAND_load_file:Cannot open file:../crypto/rand/randfile.c:88:Filename=/home/jegan/.rnd
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:IN
State or Province Name (full name) [Some-State]:Tamil Nadu
Locality Name (eg, city) []:Hosur
Organization Name (eg, company) [Internet Widgits Pty Ltd]:TekTutor
Organizational Unit Name (eg, section) []:Software
Common Name (e.g. server FQDN or YOUR name) []:ocp.tektutor.org
Email Address []:jegan@tektutor.org

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
(jegan@tektutor.org)$ openssl x509 -req -in client_reqout.txt -days 3650 -sha256 -CAcreateserial -CA  serverca.crt -CAkey servercakey.pem -out client.crt
Signature ok
subject=C = IN, ST = Tamil Nadu, L = Hosur, O = TekTutor, OU = Software, CN = ocp.tektutor.org, emailAddress = jegan@tektutor.org
Getting CA Private Key
(jegan@tektutor.org)$ ls
client.crt  client_reqout.txt  servercakey.pem  server.crt  server_reqout.txt
client.key  serverca.crt       serverca.srl     server.key
(jegan@tektutor.org)$ ls -l
total 36
-rw-rw-r-- 1 jegan jegan 1346 Aug 11 17:05 client.crt
-rw------- 1 jegan jegan 1679 Aug 11 17:02 client.key
-rw-rw-r-- 1 jegan jegan 1070 Aug 11 17:02 client_reqout.txt
-rw-rw-r-- 1 jegan jegan 1468 Aug 11 16:52 serverca.crt
-rw------- 1 jegan jegan 1675 Aug 11 16:50 servercakey.pem
-rw-rw-r-- 1 jegan jegan   41 Aug 11 17:05 serverca.srl
-rw-rw-r-- 1 jegan jegan 1346 Aug 11 17:00 server.crt
-rw------- 1 jegan jegan 1679 Aug 11 16:57 server.key
-rw-rw-r-- 1 jegan jegan 1070 Aug 11 16:59 server_reqout.txt
</pre>


## Let's create configmap with the root CA Certifacte used to sign the wildcard certificate
```
oc create configmap tektutor-ca --from-file=ca-bundle.crt=serverca.crt -n openshift-config
```

Expected output
<pre>
(jegan@tektutor.org)$ oc create configmap tektutor-ca --from-file=ca-bundle.crt=serverca.crt -n openshift-config
configmap/tektutor-ca created
</pre>

Let's create a secret that contains the wildcard certificate chain and key
```
oc create secrete tls tektutor --cert=client.crt --key=client.key -n openshift-ingress
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc create secret tls tektutor --cert=client.crt --key=client.key -n openshift-ingress</b>
secret/tektutor created
</pre>

## Patch Ingress Controller with our tektutor secret
```
oc patch ingresscontroller.operator default --type=merge -p '{"spec":{"defaultCertificate": {"name": "tektutor"}}}' -n openshift-ingress-operator
```

Expected output
<pre>
(jegan@tektutor.org)$ oc patch ingresscontroller.operator default --type=merge -p '{"spec":{"defaultCertificate": {"name": "tektutor-updated"}}}' -n openshift-ingress-operator
ingresscontroller.operator.openshift.io/default patched
</pre>
