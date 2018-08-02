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
        
        stage('Login to Pivotal Cloud Foundry') {
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'pivotaluser', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                sh 'cf login -u $USERNAME -p $PASSWORD -a $ENDPOINT -o $ORG -s $SPACE'
                    }
                }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
