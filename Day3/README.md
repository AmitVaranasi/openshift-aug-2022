# Day 3

## Login to OpenShift from command line
<pre>
(jegan@tektutor.org)$ cat ~/openshift.txt 
RedHat OpenShift CLI Login URL
++++++++++++++++++++++++++++++
https://api.ocp.tektutor.org:6443 

RedHat OpenShift web-console 
++++++++++++++++++++++++++++
https://console-openshift-console.apps.ocp.tektutor.org 

Login Credentials
++++++++++++++++++++++++++++++++++++++
+ user    | kubeadmin		     +
+ password| 6ssow-q4UhD-82pCd-FE2XL  +
++++++++++++++++++++++++++++++++++++++
(jegan@tektutor.org)$ oc login -u kubeadmin https://api.ocp.tektutor.org:6443
Authentication required for https://api.ocp.tektutor.org:6443 (openshift)
Username: kubeadmin
Password: 
Login successful.

You have access to 66 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "jegan".
</pre>

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

## Let's clean up all resources by deleting our project and recreate the same project
```
oc delete project jegan
oc new-project jegan
```

## Understanding dry-run
```
oc create deploy nginx --image=bitnami/nginx:latest --replicas=3 --dry-run=client -o yaml
```
Expected output
<pre>
(jegan@tektutor.org)$ oc create deploy nginx --image=bitnami/nginx:latest --replicas=3 --dry-run=client -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx
    spec:
      containers:
      - image: bitnami/nginx:latest
        name: nginx
        resources: {}
status: {}
</pre>

## Creating a nginx deployment 
```
oc create deploy nginx --image=bitnami/nginx:latest --replicas=3 --dry-run=client -o yaml > nginx-deploy.yml
```

## Scale up nginx deployment from 3 Pods to 6 Pods using imperative style
```
oc scale deploy/nginx --replicas=6
```

Expected ouput
<pre>
(jegan@tektutor.org)$ <b>oc scale deploy/nginx --replicas=6</b>
deployment.apps/nginx scaled
(jegan@tektutor.org)$ oc get po
NAME                     READY   STATUS              RESTARTS   AGE
nginx-78644964b4-2w2rs   1/1     Running             0          4m33s
nginx-78644964b4-4j469   0/1     ContainerCreating   0          3s
nginx-78644964b4-hgtwm   1/1     Running             0          4m33s
nginx-78644964b4-swv9w   0/1     ContainerCreating   0          3s
nginx-78644964b4-vtvb9   0/1     ContainerCreating   0          3s
nginx-78644964b4-z4znv   1/1     Running             0          4m33s
</pre>

## Scale up nginx deploying from 6 Pods to 8 Pods using declarative style
Edit nginx-deploy.yml and update the replicas count from 6 to 8
```
oc apply -f nginx-deploy.yml
```

<pre>
(jegan@tektutor.org)$ vim nginx-deploy.yml 
(jegan@tektutor.org)$ oc apply -f nginx-deploy.yml 
deployment.apps/nginx configured
(jegan@tektutor.org)$ oc get po
NAME                     READY   STATUS              RESTARTS   AGE
nginx-78644964b4-2w2rs   1/1     Running             0          6m27s
nginx-78644964b4-4j469   1/1     Running             0          117s
nginx-78644964b4-fjhsc   0/1     ContainerCreating   0          3s
nginx-78644964b4-hgtwm   1/1     Running             0          6m27s
nginx-78644964b4-swv9w   1/1     Running             0          117s
nginx-78644964b4-vtvb9   1/1     Running             0          117s
nginx-78644964b4-wpsfs   0/1     ContainerCreating   0          3s
nginx-78644964b4-z4znv   1/1     Running             0          6m27s
</pre>

## Creating ClusterIP Service using declarative style
<pre>
(jegan@tektutor.org)$ <b>oc expose deploy/nginx --port=8080 --dry-run=client -o yaml > nginx-clusterip-svc.yml</b>
(jegan@tektutor.org)$ </b>ls</b>
<b>nginx-clusterip-svc.yml</b>  nginx-deploy.yml  README.md
(jegan@tektutor.org)$ oc get svc
No resources found in jegan namespace.
(jegan@tektutor.org)$ <b>oc apply -f nginx-clusterip-svc.yml</b>
service/nginx created
(jegan@tektutor.org)$ <b>oc get svc</b>
NAME    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
nginx   ClusterIP   172.30.150.178   <none>        8080/TCP   5s
(jegan@tektutor.org)$ <b>oc describe svc/nginx</b>
Name:              nginx
Namespace:         jegan
Labels:            app=nginx
Annotations:       <none>
Selector:          app=nginx
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                172.30.150.178
IPs:               172.30.150.178
Port:              <unset>  8080/TCP
TargetPort:        8080/TCP
Endpoints:         10.128.0.111:8080,10.128.2.17:8080,10.128.2.18:8080 + 5 more...
Session Affinity:  None
Events:            <none>
</pre>

## Deleting the clusterip service using declarative style
<pre>
(jegan@tektutor.org)$ <b>oc get svc</b>
NAME    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
nginx   ClusterIP   172.30.150.49   <none>        8080/TCP   3s
(jegan@tektutor.org)$ <b>oc delete -f nginx-clusterip-svc.yml</b>
service "nginx" deleted
(jegan@tektutor.org)$ <b>oc get svc</b>
No resources found in jegan namespace.
</pre>

## Creating NodePort Service using declarative style
<pre>
(jegan@tektutor.org)$ <b>oc expose deploy/nginx --type=NodePort --port=8080 --dry-run=client -o yaml > nginx-nodeport-svc.yml</b>
(jegan@tektutor.org)$ <b>ls</b>
nginx-clusterip-svc.yml  nginx-deploy.yml  <b>nginx-nodeport-svc.yml</b>  README.md
</pre>

## Creating LoadBalancer Service using declarative style
<pre>
(jegan@tektutor.org)$ <b>oc expose deploy/nginx --type=LoadBalancer --port=8080 --dry-run=client -o yaml > nginx-lb-svc.yml</b>
(jegan@tektutor.org)$ <b>ls</b>
nginx-clusterip-svc.yml  nginx-deploy.yml  <b>nginx-lb-svc.yml</b>  nginx-nodeport-svc.yml  README.md
</pre>
