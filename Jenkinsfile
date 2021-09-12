pipeline {
   agent any
      stages {
          stage('clone the git') {
             steps {
                sh 'rm -rf dockertest1'
                sh 'git clone https://github.com/umeshkumar220/dockertest1.git'
             }
          }
          stage('build docker image') {
             steps {
                sh 'cd /var/lib/jenkins/workspace/pipeline1/dockertest1'
                sh ' cp  /var/lib/jenkins/workspace/pipeline1/dockertest1/* /var/lib/jenkins/workspace/pipeline1'
                sh 'docker build -t umeshdocker1/pipelinetest2:v2 .'
             }
          }
          stage('push image to docker hub') {
             steps {
                sh 'docker push umeshdocker1/pipelinetest2:v2'
             }
          }
          stage('deploy to docker host') {
             steps {
                sh 'docker -H tcp://10.1.3.231:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 umeshdocker1/pipelinetest2:v2'
             }
          }
          stage('check webapp rechability') {
             steps {
                sh 'sleep 10s'
                sh 'curl http://ec2-3-16-25-200.us-east-2.compute.amazonaws.com:9000'
             }
          }
     }
}      
