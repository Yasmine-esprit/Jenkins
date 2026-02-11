pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/Yasmine-esprit/Jenkins.git' 
        BRANCH = 'main' 
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo "Cloning repo ${REPO_URL} branch ${BRANCH}"
                sh "git clone -b ${BRANCH} ${REPO_URL} repo"
            }
        }

        stage('Build') {
            steps {
                echo 'Building Spring Boot project...'
                dir('repo') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                dir('repo') {
                    sh 'mvn test'
                }
            }
        }

        stage('Show Results') {
            steps {
                dir('repo') {
                    echo 'Listing compiled classes and test reports:'
                    sh 'ls -l target/classes'        
                    sh 'ls -l target/surefire-reports' 
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            deleteDir() 
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
