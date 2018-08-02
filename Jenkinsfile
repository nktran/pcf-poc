pipeline {
    agent any
    stages {
        stage('Checkout source') {
            git url: 'git://github.com/nktran/pcf-poc.git
            checkout scm
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
