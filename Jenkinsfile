pipeline {
    agent {
        docker {
            image 'node:9'
        }
    }

    options {
        timeout(time: 10, unit: 'MINUTES')
        ansiColor('xterm')
    }
    stages {
        stage('Install') {
            steps {
                sh 'npm install'
                sh 'npx bower install --allow-root'
            }
        }
        stage('Test') {
            steps {
                sauce('sauce_minecraft_gavinmogan') {
                    sh 'npm run test'
                }
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            when {
                branch 'master'
            }
            environment {
                SURGE = credentials('halkeye-surge')
            }
            steps {
                sh 'SURGE_LOGIN=$SURGE_USR SURGE_TOKEN=$SURGE_PSW npx surge -p build/es6-bundled -d minecraft.gavinmogan.com'
            }
        }
    }
}
