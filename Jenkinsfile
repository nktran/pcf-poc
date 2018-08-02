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
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'pivotaluser', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']])
                sh 'echo uname=$USERNAME pwd=$PASSWORD'
                    }
                }
        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
