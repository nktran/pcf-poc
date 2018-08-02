pipeline {
    agent any
    stages {
        stage('Checkout source') {
            steps {
                checkout scm
                git credentialsId: 'github.com', url: 'https://github.com/nktran/pcf-poc.git', branch: 'master'
            }
         }
        
        stage('Clean and Build Web Application') {
            steps {
                sh 'mvn clean package -q'
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
                sh 'cf push hotels -p $WORKSPACE/target/hotels-0.0.1-SNAPSHOT.jar --random-route'
            }
        }
        
        stage('Archive deployment package, if successful') {
            steps {
                archiveArtifacts artifacts: '$WORKSPACE/target/*.jar', onlyIfSuccessful: true
            }
        }
        
        stage('Delete Web Applcation to PCF') {
            steps {
                sh 'cf delete hotels -r -f'
            }
        }
        
    }
