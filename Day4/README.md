# Day 4

## Pod port-forwarding for quick test
```
oc port-forward pod/nginx-78644964b4-xqp77 8080:8080
```

In the above command, port 8080 that appears on the left side is the port on the local machine.

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc port-forward pod/nginx-78644964b4-xqp77 8080:8080</b>
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
Handling connection for 8080
</pre>

