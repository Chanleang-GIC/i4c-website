pipeline {
    agent any // windows agent, Jenkins-Laravel (other machine)
    
    stages {
        stage('Fetch from GitHub') { // build steps
            steps {
                echo 'Fetching from GitHub'
                git branch: 'main', url:'https://github.com/Chanleang-GIC/i4c-website.git'
            }
        }
        stage('Build using Tools') {
            steps {
                echo 'Compiling code...'
                sh 'composer install & cp .env.example .env & php artisan key:generate & npm i'
            }
        }
        stage('Test the app') {
            steps {
                echo 'Testing unit tests...'
                echo 'Testing features...'
                sh 'php artisan test'
            }
        }
        stage('Email Notification') {
            steps {
                emailext body: 'Hi, Welcome to Jenkins Alert. The build has failed.',
                         subject: 'Jenkins Build Failure',
                         to: 'chanleang7779@gmail.com'
            }
        }
    }
    
    post {
        failure {
            echo 'Sending email notification from Jenkins'

            emailext body: 'Hi, Welcome to Jenkins Alert. The build has failed.',
                subject: 'Jenkins Build Failure',
                to: 'chanleang7779@gmail.com'
        }
    }
}
