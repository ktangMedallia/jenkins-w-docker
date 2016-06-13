# jenkins-w-docker

Custom Jenkins docker image with Docker enabled, based on http://container-solutions.com/running-docker-in-jenkins-in-docker/

For MacOSX, extra steps
- use dockerenv.sh to pass in docker-machine env settings
- map .docker folder for certificate access

$ docker-machine env | sed -e 's/Users\/ktang/var\/jenkins_home/g' > /Users/ktang/jenkinsd/dockerenv.sh
$ chmod +x /Users/ktang/jenkinsd/dockerenv.sh
$ docker build -t jenkinsd .
$ docker run -p 8080:8080 -p 50000:50000 -v /Users/ktang/jenkinsd:/var/jenkins_home -v $(which docker):/usr/bin/docker -v /Users/ktang/.docker:/var/jenkins_home/.docker jenkinsd

Then, Jenkins job build should be able to access Docker like this
  . /var/jenkins_home/dockerenv.sh
  docker ps

