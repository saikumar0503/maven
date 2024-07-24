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
                sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war  ec2-user@172.16.10.26:/home/ec2-user/apache-tomcat-9.0.46/webapps/
                    
                    ssh ec2-user@172.16.10.26 /home/ec2-user/apache-tomcat-9.0.46/bin/shutdown.sh
                    
                    ssh ec2-user@172.16.10.26 /home/ec2-user/apache-tomcat-9.0.46/bin/startup.sh
                
                """

                }
            }
        }
    }
}
