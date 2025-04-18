pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Building..."
                sh 'docker build -f Dockerfile.build -t lab02-build .'
                sh 'docker run --rm lab02-build'
            }
        }
        stage('Test') {
            steps {
                echo "Testing..."
               sh 'docker build -f Dockerfile.test -t lab02-test . 2>&1 | tee test-build-${BUILD_NUMBER}.log'
               sh 'docker run --rm lab02-test 2>&1 | tee test-run-${BUILD_NUMBER}.log'
            }
        }
         stage('Archive') {
            steps {
                echo "Archiving..."
                archiveArtifacts artifacts: 'test-*.log', fingerprint: true

            }
        }
        
    }
    
}
