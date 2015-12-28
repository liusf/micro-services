Setup Referrence: http://philzim.com/2014/11/12/service-discovery-orchestration-with-mesos-and-consul/

#### 安装docker (CentOS 7)
https://docs.docker.com/engine/installation/

```
sudo yum update
sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
[dockerrepo]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/centos/$releasever/
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
EOF
sudo yum install docker-engine
sudo usermod -aG docker your_username
sudo chkconfig docker on
```

#### 安装Consul
https://releases.hashicorp.com/consul/
```
wget https://releases.hashicorp.com/consul/0.6.0/consul_0.6.0_linux_amd64.zip
unzip consul_0.6.0_linux_amd64.zip
sudo cp consul /usr/local/bin
## 启动consul
consul agent 
```
#### 安装Consul-template
https://releases.hashicorp.com/consul-template/
```
wget https://releases.hashicorp.com/consul-template/0.12.0/consul-template_0.12.0_linux_amd64.zip
unzip consul-template_0.12.0_linux_amd64.zip
sudo cp consul-template /usr/local/bin
```
#### 安装haproxy
```
sudo yum install haproxy
```
#### docker的host上开启Registrator
https://hub.docker.com/r/gliderlabs/registrator/
```
docker pull gliderlabs/registrator
docker run -d \
    --name=registrator \
    --net=host \
    --volume=/var/run/docker.sock:/tmp/docker.sock \
    gliderlabs/registrator:latest \
      consul://localhost:8500
```
