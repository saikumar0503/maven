pipeline {
    agent any
    environment {
        PATH = "/usr/local/apache-maven-3.8.1/bin:${env.PATH}"
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'master', credentialsId: 'IAS-new', url: 'https://github.com/saikumar0503/maven.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Dev') {
            steps {
                sshagent(['ec2-user']) {
                    sh 'scp -o StrictHostKeyChecking=no target/project-100-1.0-SNAPSHOT.jar ec2-user@172.16.10.251:/home/ec2-user/apache-tomcat-9.0.46/webapps/'
                }
            }
        }
    }
}
