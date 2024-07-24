pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/saikumar0503/maven.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Dev') {
            steps {
                sshagent(['IAS-one']) {
                    sh 'scp -o StrictHostKeyChecking=no target/project-z-1.0-SNAPSHOT.jar ec2-user@172.16.10.251:/home/ec2-user/apache-tomcat-9.0.46/webapps/'
                    sh'ssh ec2-user@172.16.10.26 /home/ec2-user/apache-tomcat-9.0.46/bin/shutdown.sh'
                    sh'ssh ec2-user@172.16.10.26 /home/ec2-user/apache-tomcat-9.0.46/bin/startup.sh'
                }
            }
        }
    }
}
