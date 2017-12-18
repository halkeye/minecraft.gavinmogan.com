properties([[$class: 'GithubProjectProperty', displayName: '', projectUrlStr: 'https://github.com/halkeye/minecraft.gavinmogan.com/']])

pipeline {
    agent any

    options {
        timeout(time: 10, unit: 'MINUTES')
        ansiColor('xterm')
    }
    stages {
        stage('Install') {
            steps {
                sh 'npm install'
                sh 'npx bower install'
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
