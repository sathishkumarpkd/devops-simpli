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

