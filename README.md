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



