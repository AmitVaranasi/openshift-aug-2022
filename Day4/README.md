# Day 4

## Pod port-forwarding for quick test
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

## See if you can access the web page from the Pod after port-forward in a different terminal
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

## Listing the secrets
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

## See if you can print the value stores in the secrets using describe command
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
