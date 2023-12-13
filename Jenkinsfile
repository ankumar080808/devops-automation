pipeline {
    agent any

    stages {
        stage('Checkout and Build') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ankumar080808/devops-automation.git']])
                bat 'mvn clean install'
            }
        }
        
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t ankumar0808/devops-integration .'
                }
            }
        }
        
        stage('Push image to Hub'){
            steps{
                script{
                 withCredentials([usernameColonPassword(credentialsId: 'ankumar0808', variable: 'DOCKER_CREDENTIALS')]) {
   
                    def credentials = DOCKER_CREDENTIALS.split(':')
                def username = credentials[0]
                def password = credentials[1]

                // Docker login
                bat "docker login -u ${username} -p ${password}"

                // Docker push
                bat 'docker push ankumar0808/devops-integration'
             
                     
                 }
                   
                 
            }
        }
     }

    
    
    
}
}