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

