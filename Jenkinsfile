pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('Prepare') {
            agent {
                docker { image 'node:alpine' }
            }
            steps {
                echo 'Prepare'
                dir('code/frontend'){
                     sh 'npm install'
                }
                dir('code/backend'){
                     sh 'npm install'
                }

            }
        }
        stage('Build') {
            agent {
                docker { image 'node:alpine' }
            }
            steps {
                echo 'Build'      
                dir('code/frontend'){
                     sh 'npm run build'
                }
                dir('code/backend'){
                    sh 'npm run build'
                }
            }
        }
        stage('Static Analysis') {
            agent {
                docker { image 'node:alpine' }
            }
            steps {
                echo 'Analyze' 
                 dir('code/frontend'){
                     sh 'npm run lint'
                }
                dir('code/backend'){
                    sh 'npm run lint'
                }
            }
        }
        stage('Unit Test') {
            agent {
                docker { image 'node:alpine' }
            }
            steps {
                echo 'Test'
                  dir('code/backend'){
                    sh 'npm run test'
                    }
            }
        }
        stage('e2e Test') {
            steps {             
                echo 'e2e Test'
            }
            post {
                always {
                    echo 'Cleanup'
                }
            }
        }
        stage('Deploy') {
            steps {                
                echo 'Deploy'
            }
        }
    }
}
