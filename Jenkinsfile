pipeline {
    agent any
    tools {
        maven 'maven' 
    }
    stages{    
       stage('Initialize'){
          steps{
            sh 'echo "PATH = ${PATH}"'
            sh 'echo "M2_HOME = ${M2_HOME}"'
          }
       }
       stage('Checkout stage'){
          steps{
            git 'https://github.com/kpraju123/java-hello-world-webapp.git'
          }
       }
       stage('Build-stage'){
          steps{
            sh 'mvn clean package'
            sh 'mv target/*.war target/demo.war'
          }
       }
       stage('Deploy-stage'){
          steps{
            sshagent(['ec2-id']) {
            sh '''scp -o Stricthostkeychecking=no target/demo.war ubuntu@172.31.39.34:/var/lib/tomcat9/webapps'''
            }
          }
       }
    }
}
