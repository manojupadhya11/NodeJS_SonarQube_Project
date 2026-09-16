pipeline {
    agent any
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('git-checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/manojupadhya11/NodeJS_SonarQube_Project.git'
            }
        }
        stage('dependencies') {
            steps {
                nodejs('nodejs26') {
                    sh 'rm -rf node_modules package-lock.json'
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                nodejs('nodejs26') {
                    sh 'npm test'
                }
            }
        }
    stage('Sonar') {
        steps {
            withSonarQubeEnv('sonar') {
                sh '''$SCANNER_HOME/bin/sonar-scanner \
                -Dsonar.projectKey=NodeJS-SonarQube-Project \
                -Dsonar.projectName=NodeJS-SonarQube-Project \
                -Dsonar.sources=. \
                -Dsonar.tests=. \
                -Dsonar.test.inclusions=**/*.test.js \
                -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info'''
        }
    }
}
    }
}
