
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Jenkins has checked out the GitHub repository.'
            }
        }

        stage('Build') {
            steps {
                echo 'Build stage is running.'
                sh 'pwd'
                sh 'git --version'
            }
        }

        stage('Test') {
            steps {
                echo 'Test stage is running.'
            }
        }

        stage('Finish') {
            steps {
                echo 'GitHub and Jenkins integration successful!'
            }
        }
    }
}
