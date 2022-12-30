pipeline {
    agent any

    

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', credentialsId: 'git_credentials', url: 'https://github.com/valipisanthi/saidevopsimp.git'

                // Run Maven on a Unix agent.
                sh "mvn clean install"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('deploy') {
            steps {
                sshagent(['deploy-jar']) {
                   sh 'scp -o StrictHostKeyChecking=no target/gamutgurus.war  ec2-user@13.234.30.116:/home/ec2-user/apache-tomcat-9.0.70/webapps'
                }   
            }
            
        }  
        
        stage('docker build') {
            steps {
                script {
                   sh 'docker build -t valipireddy1994/test .'
                }   
            }
            
        }  
        
        stage('docker push') {
            steps {
                script {
                   sh 'docker login -u "valipireddy1994" -p "12345scm@" docker.io'
                   sh 'docker push  valipireddy1994/test'
                }   
            }
            
        }  
    }
}

