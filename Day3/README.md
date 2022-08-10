# Day 3

## Creating NodePort external Service
Delete any existing service for nginx
```
oc delete svc/nginx
```

Expected ouptut
<pre>
(jegan@tektutor.org)$ oc expose deploy/nginx --type=NodePort --port=8080
service/nginx exposed
(jegan@tektutor.org)$ oc get svc
NAME    TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
nginx   NodePort   172.30.40.251   <none>        8080:32000/TCP   3s
(jegan@tektutor.org)$ oc describe svc/nginx
Name:                     nginx
Namespace:                jegan
Labels:                   app=nginx
Annotations:              <none>
Selector:                 app=nginx
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       172.30.40.251
IPs:                      172.30.40.251
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  32000/TCP
Endpoints:                10.128.2.16:8080,10.129.1.8:8080,10.131.0.17:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
(jegan@tektutor.org)$ virsh list
 Id    Name                           State
----------------------------------------------------
 2     ocp-lb                         running
 10    ocp-master-1                   running
 11    ocp-master-2                   running
 12    ocp-master-3                   running
 13    ocp-worker-1                   running
 14    ocp-worker-2                   running

(jegan@tektutor.org)$ oc get nodes -o wide
NAME                        STATUS   ROLES           AGE   VERSION           INTERNAL-IP       EXTERNAL-IP   OS-IMAGE                                                        KERNEL-VERSION                 CONTAINER-RUNTIME
master-1.ocp.tektutor.org   Ready    master,worker   28h   v1.23.5+012e945   192.168.122.245   <none>        Red Hat Enterprise Linux CoreOS 410.84.202207262020-0 (Ootpa)   4.18.0-305.57.1.el8_4.x86_64   cri-o://1.23.3-11.rhaos4.10.gitddf4b1a.1.el8
master-2.ocp.tektutor.org   Ready    master,worker   28h   v1.23.5+012e945   192.168.122.121   <none>        Red Hat Enterprise Linux CoreOS 410.84.202207262020-0 (Ootpa)   4.18.0-305.57.1.el8_4.x86_64   cri-o://1.23.3-11.rhaos4.10.gitddf4b1a.1.el8
master-3.ocp.tektutor.org   Ready    master,worker   28h   v1.23.5+012e945   192.168.122.70    <none>        Red Hat Enterprise Linux CoreOS 410.84.202207262020-0 (Ootpa)   4.18.0-305.57.1.el8_4.x86_64   cri-o://1.23.3-11.rhaos4.10.gitddf4b1a.1.el8
worker-1.ocp.tektutor.org   Ready    worker          28h   v1.23.5+012e945   192.168.122.101   <none>        Red Hat Enterprise Linux CoreOS 410.84.202207262020-0 (Ootpa)   4.18.0-305.57.1.el8_4.x86_64   cri-o://1.23.3-11.rhaos4.10.gitddf4b1a.1.el8
worker-2.ocp.tektutor.org   Ready    worker          28h   v1.23.5+012e945   192.168.122.197   <none>        Red Hat Enterprise Linux CoreOS 410.84.202207262020-0 (Ootpa)   4.18.0-305.57.1.el8_4.x86_64   cri-o://1.23.3-11.rhaos4.10.gitddf4b1a.1.el8
(jegan@tektutor.org)$ curl 192.168.122.245:32000
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
(jegan@tektutor.org)$ curl 192.168.122.197:32000
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
