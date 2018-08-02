pipeline {
    agent any
    stages {
        stage('Checkout source') {
            steps {
                checkout scm
                git credentialsId: 'github.com', url: 'https://github.com/nktran/pcf-poc.git', branch: 'master'
                }
            }
        
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn clean package'
                }
            }
        
        stage('Deploy to Pivotal Cloud Foundry') {
            steps {
                    withCredentials([string(credentialsId: 'nktran75', variable: 'password')])
                    echo '$password'
                    }
                }
        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
