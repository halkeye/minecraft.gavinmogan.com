properties([[$class: 'GithubProjectProperty', displayName: '', projectUrlStr: 'https://github.com/halkeye/minecraft.gavinmogan.com/']])

pipeline {
    agent {
        node { 
            label ''
        }
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
                    sauceconnect(options: '', sauceConnectPath: '') {
                        sh 'npm run test'
                    }
                }
            }
        }
        
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
    }
}
