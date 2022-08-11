# OpenShift

## Installing Docker Community Edition in CentOS 7.x
```
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
```

## RedHat Developer Sandbox ( Openshift on cloud for learning purpose )
<pre>
https://developers.redhat.com/developer-sandbox
</pre>

## Code Ready Containers
Installing OpenShift in your Laptop/Desktop
<pre>
https://developers.redhat.com/products/openshift-local/overview
</pre>
