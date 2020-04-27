-GIT Commands:
-Jenkins:


GIT Commands:
============
ssh-keygen -t rsa -C “sathishkumarpkd@gmail.com”
gedit id_rsa.pub

sathishkumarpkd@sathishkumarpkd:~/devops-simpliLesson2$
/home/sathishkumarpkd/.ssh/id_rsa


curl wgetip.com
mkdir gitrepo
cd gitrepo/
ls -lart
git init
ls -lart
ls -lart .git/

//Roll back entire directory
git reset --hard
//Roll back <filename>
git checkout <filename>
//Roll back <commitID>
git revert 9d378bf78495c1f3aabd78e7bf
//Roll back <commitID> : and removed form History.
git reset --hard <commitID>
git log

//Create develop branch from default master.
// edit the file and commit to develop branch.
git branch -l
git branch develop
git checkout develop
git branch -l
git log
echo "Develop Branch" >> README.txt
cat README.txt
git add README.txt
git commit -m "Develop Commit"
git log

//switch to master branch, and merge code from develop branch
git checkout master
git branch -l
git log
git merge develop
git log

// with github push, push to remote repo.
git remote add origin https://github.com/sathishkumarpkd/sample.git
git push -u origin master

//git pull origin master
git pull  origin master

git tag v1.0
git tag -l
git push --tags

//Jenkins installation.
 url:https://pkg.jenkins.io/debian-stable/

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
echo "deb https://pkg.jenkins.io/debian-stable binary/" > /etc/apt/sources.list.d/jenkins.list
apt update
apt install openjdk-8-jdk
apt install jenkins
service jenkins status
service jenkins restart  (In case service is not active) 

curl wgetip.com
http://104.43.195.118:8080/
cat /var/lib/jenkins/secrets/initialAdminPassword
	dde984ded38442c4972b300002de32c1
	
//Jenkins


git clone https://github.com/anujdevopslearn/MavenBuild.git
cd MavenBuild/
apt install maven
mvn clean
mvn clean install

// after forking from trainer
https://github.com/sathishkumarpkd/MavenBuild.git

//Payload URL in GitHub for webhook
http://40.122.34.228:8080/github-webhook/

// Secret token generated in Jenkins.(admin->configure->generatetoken with GitHub)
111e3b3435d4294ad530134138fe178209

//for practice
https://github.com/jitpack/maven-simple
from Anuj Sharma to All Participants:
// Jenkins pipeline.
https://github.com/jenkins-docs/simple-java-maven-app
https://github.com/jenkinsci/pipeline-examples/tree/master/jenkinsfile-examples

//Junit
https://github.com/jitpack/maven-simple
https://github.com/jitpack/maven-simple.git
Lesson4 demo for Cucumebr config.

//Ansible
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
ansible --version
cd /etc/ansible
vi ansible.cfg
42006 : edit remote port for simplilearn in ansible.cfg.

https://github.com/anujdevopslearn/InterviewQuestions/blob/master/InstallationGuides/Ansible.txt
//centos local installation.
https://www.linuxtechi.com/manage-windows-host-using-ansible/

cat ansible.cfg | grep 42006
remote_port    = 42006

//dynamic ip addr on host:
https://github.com/sermilrod/ansible-dynamic-inventory

vi /etc/ansible/hosts
uncomment following servers : Grouped and Ungrouped.

# Ex 1: Ungrouped hosts, specify before any group headers.
green.example.com
# Ex 2: A collection of hosts belonging to the 'webservers' group
[webservers]
alpha.example.org
beta.example.org
# Ex 3: A collection of database servers in the 'dbservers' group
[dbservers]
db01.intranet.mydomain.net

//cat hosts : to show the edits done
// perform the ping operations: it should fail.
 ansible -m ping webservers
 ansible -m ping dbservers
 ansible -m ping green.example.com
 ansible -m ping green.example.com1

//failed ping
green.example.com | UNREACHABLE! => {
    "changed": false, 
    "msg": "Failed to connect to the host via ssh: ssh: Could not resolve hostname green.example.com: Name or service not known", 
    "unreachable": true

//to make it pass key has to be generated and add that key to client in  authorized_keys

// generate key
ssh-keygen -t rsa
ls -lart /root/.ssh/

// public key //cat /root
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC3sjPlyCp3U1nYmPWhCKJbkxjVYg0twnRExG71yI5C2/wwvvsVHhoIrIF/e+xKbX23LblLidL8F78CYed2vSpQYnOjJmyPTEjGRP9G8cMt63gajKiDixrf4OQRftAbPc3uhrjHwn8Q3OJMF6ERM59JiQPDAKMalx90KeLzHePX4/i3jVo6FwM2r59kOSooIuFovKDD6A7E693d0PPZCpjuB2h13jceoJ5xW3aj/+ZgNtbxClJ2AVaMzk1LjEoyRSjvvFFboAhQgGjfRSOgEfdw8xPj5DkJD3W4GFLhFz9v8P7MYU1vsjOn06h6qF+3uuY+CCMENDYl3r6jHybZvCX/ root@sathishkumarpkd

// on same machine server client.
// copy the pub key(from master) to authorized_keys(client)
// here its same machine,
cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
ssh -p 42006 localhost "hostname"
// returns sathishkumarpkd

// edit the hosts
vi /etc/ansible/hosts
add localhost .
and execute : ansible -m ping localhost
// returns success.

//launchpad.net/ansible
// diffreent modules and categories
https://docs.ansible.com/ansible/latest/modules/modules_by_category.html

//ansible module demo.
//get yml file(playbook) from git
//this will install apache server in local host.
//this local host was saved in hosts.config earlier, under webserver group.
//in real time, all the servers are to be mentioned in webserver group.

wget https://gist.githubusercontent.com/anujdevopslearn/8395705058c9cd4f4f5c3fec5591b246/raw/ca103bfd5a8791c805aaed30efc9c2cb192e7e72/apache.yml
ansible-playbook apache.yml

//Instead of chnaging ansible.cfg for remote port and user, we can update in hosts.cfg.
localhost ansible_port=42006 ansible_user=root(or any user like root permission)

//adhoc commands for single line execution:
// This is used instead of playbook
ansible -m shell -a "service apache2 status" webservers
ansible -m shell -a "apt -y install dos2unix" webservers

// mysql installation.
wget https://gist.githubusercontent.com/anujdevopslearn/98a73c0ef7f72a70fc11759f8b2b9c25/raw/344bd206c7dbadfd56f32dc755c06e450c9b0d0f/mysql.yml
ansible-playbook mysql.yml
ansible -m shell -a "service apache2 status" webservers

// for autoscaling in AWS
https://github.com/sermilrod/ansible-dynamic-inventory

// for tomcat installation
wget https://gist.githubusercontent.com/anujdevopslearn/efa28700a3b8aca18d2866aa2d24fa02/raw/a48022c9b6111a668fcc9f3f3c63928ea2840db0/TomcatInstallation.yml
ansible-playbook TomcatInstallation.yml
ansible -m shell -a "service tomcat status" webservers

//ansible module for docker
https://docs.ansible.com/ansible/2.6/modules/list_of_cloud_modules.html#docker

//Docker
apt update
apt install docker.io
service docker restart
docker version
docker pull ubuntu
docker images
docker rmi ubuntu:18.04 // remove image

// run the container,the root user at Host machine will be changed to 
// ubuntu container, since this is trimmed version, ot of Ubuntu commands wont work, 
// but we can install one by one.
// root@sathishkumarpkd:~#  to root@a9b325b6e811:/#
docker run -it ubuntu bash
// docker commands wont work inside ubuntu container.
>exit

// shows this container id, which is in exit status.
docker ps -a
//-d detach, is diffrent from -it, as we stay in root@hostmachine itself.
docker run -d jenkins
// same above but,name is provided.
docker run --name dev_jenkins -d jenkins

//docker exec -it sath_dev_jenkins bash
//cat /var/lib/jenkins_home/secrets/initialAdminPassword

docker ps
docker stop 515328e2e454
docker ps
docker restart 515328e2e454
docker ps
docker rm 515328e2e454  -f

// to access from outside world.
// -p hostport:container port

docker run --name prod_jenkins -d -p 8080:8080 jenkins
docker ps
docker run --name dev_jenkins -d -p 80:8080 jenkins
docker ps
curl wgetip.com

// home work for Nagios installation.
https://github.com/anujdevopslearn/InterviewQuestions/blob/master/InstallationGuides/CleanServices.txt
Run Commands from root ID:    14-23
https://assets.nagios.com/downloads/nagiosxi/docs/Installing-Nagios-XI-Manually-on-Linux.pdf
curl https://assets.nagios.com/downloads/nagiosxi/install.sh | sh


// docker build
// and build an Image

 git clone https://github.com/anujdevopslearn/Docker.git
 cd Docker/
 ls -lart
 docker build -t customimage .
 docker images

////////////////////////docker file contents/////////////////////////////////////////////////
//docker file contents displayed to create Custom image.
cat Dockerfile 
FROM ubuntu

ENV DEBIAN_FRONTEND=non-interactive
# Install dependencies
RUN apt-get update -y
RUN apt-get install -y git curl apache2 php libapache2-mod-php php-mysql

# Install app
RUN rm -rf /var/www/html/*
ADD src /var/www/html/

# Configure apache
RUN a2enmod rewrite
RUN chown -R www-data:www-data /var/www/html
ENV APACHE_RUN_DIR /var/www/html
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2


EXPOSE 80

CMD ["/usr/sbin/apache2", "-D",  "FOREGROUND"]
/////////////////////////end of docker file contents/////////////////////////////////////////////////
//docker images built by above docker file.
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
customimage         latest              9c5e2eaf53ac        46 seconds ago      269MB
ubuntu              latest              1d622ef86b13        27 hours ago        73.9MB
////////////////////////////////end of docker images built by above docker file.//////////////////////

// run 
docker run -d -p 8081:80 customimage
//http://localhost:8081/ : this will accessed inside VM.

//Assignment
https://github.com/anujdevopslearn/AspDotNetDocker.git

//Docker compose install

curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

//execute docker compose
  git clone https://github.com/anujdevopslearn/DockerCompose.git
  cd DockerCompose/
  ls -alrt
  cat Dockerfile 
  mvn clean install -Dmaven.test.skip=true
  ls -alrt target
  docker-compose up -d
  docker images
  docker ps  -a

/////////////////////////////////////docker-compose.yml////////////////////////////////////////////////////////
cat docker-compose.yml 
version: '3'

services:
  db:
    image: mysql:5.7
    environment:
      - MYSQL_ROOT_PASSWORD=root123
      - MYSQL_DATABASE=spring_app_db
      - MYSQL_USER=app_user
      - MYSQL_PASSWORD=test123
  
  spring-boot-jpa-app:
    image: spring-boot-jpa-image
    build:
      context: ./
      dockerfile: Dockerfile
    depends_on:
      - db
    ports:
      - 8087:8080

//////////////////////////////////////end of docker-compose.yml/////////////////////////////////////////////////
//docker file in compose eg:
cat Dockerfile 
FROM ubuntu:18.04

RUN apt -y update && apt -y install openjdk-8-jdk maven apache2
WORKDIR /app

COPY . /app


EXPOSE 8080
LABEL maintainer=“chathuranga.t@gmail.com”
ADD ./target/spring-boot-data-jpa-example-0.0.1-SNAPSHOT.jar spring-boot-data-jpa-example-0.0.1-SNAPSHOT.jar
ENTRYPOINT ["java","-jar","spring-boot-data-jpa-example-0.0.1-SNAPSHOT.jar"]
///////////////////////////////////end of docker file in compose eg://////////////////////////////////////////

// Nagios monitoring DB
// Mysql is running in docker
docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=password mysql
// not in pubic access
docker inspect mysql | grep IPAddress

//Kubernetes installation
https://github.com/anujdevopslearn/InterviewQuestions/blob/master/InstallationGuides/CleanServices.txt
28-30
https://github.com/anujdevopslearn/InterviewQuestions/blob/master/InstallationGuides/Kubernetes.txt
3-19

//Kube cheat sheet.
http://m76.eu/cheatsheet-kubernetes-A4.pdf

//pull bootcamp image from docker hub
kubectl run kubernetes-bootcamp --image=docker.io/jocatalin/kubernetes-bootcamp:v1 --port=8080
kubectl get deployments
kubectl get pods
//////////////////////////////////////////////////////////////////
kubectl get deployments  //get deployments
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   1/1     1            1           51s

kubectl get pods  // get pods
NAME                                   READY   STATUS    RESTARTS   AGE
kubernetes-bootcamp-7dc9765bf6-4n9fm   1/1     Running   0          67s

////////////////////////////////////////////////////////////////
//
kubectl run kubernetes-jenkins --image=docker.io/jenkins:latest --port=8080
kubectl run kubernetes-nginx --image=docker.io/nginx --port=80

//get pods
  kubectl get pods
  kubectl describe pod kubernetes-bootcamp-7dc9765bf6-dfjzg
// get ip
  kubectl get pods -o wide

///////////////////////////////////Console output////////////////////
//kubectl describe pod kubernetes-bootcamp-7dc9765bf6-4n9fm
Name:           kubernetes-bootcamp-7dc9765bf6-4n9fm
Namespace:      default
Priority:       0
Node:           sathishkumarpkd/10.0.1.4
Start Time:     Sun, 26 Apr 2020 06:02:35 +0000
Labels:         pod-template-hash=7dc9765bf6
                run=kubernetes-bootcamp
Annotations:    <none>
Status:         Running
IP:             10.32.0.4
Controlled By:  ReplicaSet/kubernetes-bootcamp-7dc9765bf6
Containers:
  kubernetes-bootcamp:
    Container ID:   docker://0dec7ab466b939c4f321648890d46d0b977f3866546c52a1a7dd36d1fcfa0c94
    Image:          docker.io/jocatalin/kubernetes-bootcamp:v1
    Image ID:       docker-pullable://jocatalin/kubernetes-bootcamp@sha256:0d6b8ee63bb57c5f5b6156f446b3bc3b3c143d233037f3a2f00e279c8fcc64af
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Sun, 26 Apr 2020 06:02:57 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-fk4c2 (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  default-token-fk4c2:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-fk4c2
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason     Age   From                      Message
  ----    ------     ----  ----                      -------
  Normal  Scheduled  15m   default-scheduler         Successfully assigned default/kubernetes-bootcamp-7dc9765bf6-4n9fm to sathishkumarpkd
  Normal  Pulling    15m   kubelet, sathishkumarpkd  Pulling image "docker.io/jocatalin/kubernetes-bootcamp:v1"
  Normal  Pulled     15m   kubelet, sathishkumarpkd  Successfully pulled image "docker.io/jocatalin/kubernetes-bootcamp:v1"
  Normal  Created    15m   kubelet, sathishkumarpkd  Created container kubernetes-bootcamp
  Normal  Started    15m   kubelet, sathishkumarpkd  Started container kubernetes-bootcamp

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//kubectl get pods -o wide
NAME                                   READY   STATUS    RESTARTS   AGE   IP          NODE              NOMINATED NODE   READINESS GATES
kubernetes-bootcamp-7dc9765bf6-4n9fm   1/1     Running   0          16m   10.32.0.4   sathishkumarpkd   <none>           <none>
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//curl 10.32.0.4:8080
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp-7dc9765bf6-4n9fm | v=1

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//execute and access from outside.
kubectl exec -it kubernetes-bootcamp-7dc9765bf6-4n9fm bash
ps -ef
exit

///////////////////////////////////////////////////////////////////////////////////////////////////
//ps -ef
UID         PID   PPID  C STIME TTY          TIME CMD
root          1      0  0 06:02 ?        00:00:00 /bin/sh -c node server.js
root          7      1  0 06:02 ?        00:00:00 node server.js
root         25      0  0 06:30 pts/0    00:00:00 bash
root         32     25  0 06:31 pts/0    00:00:00 ps -ef
///////////////////////////////////////////////////////////////////////////////////////////////////////
//
kubectl expose deployment/kubernetes-bootcamp --port=8080 --target-port=8080 --type=NodePort
kubectl expose deployment/kubernetes-jenkins --port=8080 --target-port=8080 --type=NodePort
kubectl expose deployment/kubernetes-nginx --port=80 --target-port=80 --type=NodePort
//
kubectl get svc

//
  clear
  kubectl get pods
  kubectl delete pod kubernetes-bootcamp-7dc9765bf6-4n9fm
  kubectl get pods
  curl localhost:30382
// scaling to 2 pods.
  kubectl scale deployments/kubernetes-bootcamp --replicas=2
// to delete all pods
  kubectl scale deployments/kubernetes-bootcamp --replicas=0
  kubectl get pods
  kubectl get pods -o wide
//////after scaling with 2 replicas/////////////////////////////////////////////////////////////////////////////////////
kubectl get pods -o wide
NAME                                   READY   STATUS    RESTARTS   AGE   IP          NODE              NOMINATED NODE   READINESS GATES
kubernetes-bootcamp-7dc9765bf6-bf5xx   1/1     Running   0          12m   10.32.0.5   sathishkumarpkd   <none>           <none>
kubernetes-bootcamp-7dc9765bf6-tvh44   1/1     Running   0          26s   10.32.0.4   sathishkumarpkd   <none>           <none>
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
  curl localhost:30382
// set image with v2 version, so pods with v1 will get deleted automatically.
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
kubectl rollout status deployments/kubernetes-bootcamp


//project simplilearn.
https://github.com/anujdevopslearn/InterviewQuestions/tree/master/Demos
https://github.com/anujdevopslearn/InterviewQuestions/blob/master/Demos/Dockerize%20Angular%20App%20-%20Solution.docx
