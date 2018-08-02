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
                sh 'cf login -u $USERNAME -p $PASSWORD -a $API_URL -o $ORG -s $SPACE'
                    }
                }
        }
        
        stage('Deploy Web Applcation to PCF') {
            steps {
                echo 'Deploying....'
                sh 'cf push hotels -p $WORKSPACE/hotels/target/hotels-0.0.1-SNAPSHOT.jar --random-route'
            }
        }
    }
}
