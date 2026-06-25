pipeline {
agent any

stages {
    stage('Clean Workspace') {
        steps {
            cleanWs()
         }
    }

    stage('Checkout Code') {
        steps {
            checkout scm
        }
    }
    

    stage('Verify Docker') {
        steps {
            sh 'docker --version'
            sh 'docker compose version'
        }
    }

    stage('Stop Existing Containers') {
        steps {
            sh 'docker compose down || true'
        }
    }

    stage('Build Application') {
        steps {
            sh 'docker compose build --no-cache'
        }
    }

    stage('Deploy Application') {
        steps {
            sh 'docker compose up -d'
        }
    }

    stage('Check Running Containers') {
        steps {
            sh 'docker ps'
        }
    }
    
}

post {
    success {
        echo 'Deployment Successful'
    }

    failure {
        echo 'Deployment Failed'
    }
}

}
