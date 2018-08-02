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
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
