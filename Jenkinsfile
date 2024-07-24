
pipeline{
    agent any
    
    environment{
        PATH = "/opt/maven3/bin:$PATH"
    }
    stages{
        stage("Git Checkout"){
            steps{
                git credentialsId: 'IAS-new', url: 'https://github.com/saikumar0503/project-100.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("deploy-dev"){
            steps{
                sshagent(['IAS-one']) {
                sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war  ec2-user@172.16.10.251:/home/ec2-user/apache-tomcat-9.0.46/webapps/
                    
                    ssh ec2-user@172.16.10.251 /home/ec2-user/apache-tomcat-9.0.46/bin/shutdown.sh
                    
                    ssh ec2-user@172.16.10.251 /home/ec2-user/apache-tomcat-9.0.46/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}
