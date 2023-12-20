pipeline {
    agent any
    tools {
        maven '3.9.6'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ELMACHKOURIImane/JenkinsTes']])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t elmachkouriimane/devops-integration .'
                }
            }
        }
        stage('Push to docker hub') {
            steps {
                withCredentials([string(credentialsId: 'Docker', variable: 'docker')]) {
                    sh 'docker login -u elmachkouriimane -p ${docker}'
                    sh 'docker push elmachkouriimane/devops-integration'
                }
            }
        }
    }
}