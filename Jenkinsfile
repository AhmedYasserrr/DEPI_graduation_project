pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'yasserrr/depi:latest' 
        DOCKER_CREDENTIALS  = credentials('docker')
    }
    stages {
        stage('Build Docker Image') {
            agent { label 'wsl' }
            steps {
                sh 'docker build -t $DOCKER_IMAGE  ~/depi/nhorizon-java-container/'
            }
        }
        stage('Push Docker Image') {
            agent { label 'wsl' }
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                    }
                    sh "docker push $DOCKER_IMAGE"
                }
                
            }
        }
        
        stage('Pull and Run') {
            agent { label 'windows' } 
            steps {
                bat 'docker pull %DOCKER_IMAGE%'
                bat 'docker run -d -p 9090:9090 %DOCKER_IMAGE%'
                bat '''
                    @echo off
                    :pingloop
                    ping 127.0.0.1 -n 1 > nul
                    curl http://localhost:9090/ > nul 2>&1
                    if errorlevel 1 (
                        echo Waiting for service...
                        timeout /t 2 /nobreak > nul
                        goto pingloop
                    ) else (
                        echo Service is up!
                    )
                    '''
            }
        }
    }
}
