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
