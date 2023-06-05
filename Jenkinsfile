pipeline {
    agent any

     stages {
         stage('code download') {
             steps {
                 git 'https://github.com/intelliqittrainings/maven.git'
             }
         }
         stage('build the code') {
             steps {
                 sh 'mvn package'
             }
         }
         stage('copy artifact') {
             steps {
                 sh 'cp -r /home/ubuntu/.jenkins/workspace/test/webapp/target/webapp.war /home/ubuntu/.jenkins/workspace/test'
                
             }
         }
         stage('design and build dockerfile') {
             steps {
                  sh ''' 
                       cd /home/ubuntu/.jenkins/workspace/test
                       ls
                       docker build -t venkatasundeep/javaapp .
                     '''
             }
         }
         stage('push image into dockerhub'){
             steps {
                 sh 'docker login -u venkatasundeep -p Sandeep@2023'
                 sh 'docker push venkatasundeep/javaapp'
                 
             }
         }
         stage('deploy  docker image into qa servers using ansible') {
             steps {
                 sh 'ssh ubuntu@172.31.86.221 ansible-playbook playbook1.yml -b'
             }
         }
        
        stage('download and run selenium scripts') {
            steps {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/test/testing.jar'

            }
        }



}
}