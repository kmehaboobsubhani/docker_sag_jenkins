#!groovy​

pipeline {
    agent none

    options {
        buildDiscarder(logRotator(numToKeepStr:'10'))
        disableConcurrentBuilds()
    }

    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kmehaboobsubhani/SAGProject.git']]])
            }
        }

        stage("Up") {
            agent {
                label 'w64' // this is Windows pipeline
            }
           
            steps {
                unstash 'scripts'
                timeout(time:20, unit:'MINUTES') {
                    bat 'ant up -Dcc=internal -Denv=internal'
                }
            }
            post {
                success {
                    junit 'build/tests/**/TEST-*.xml'
                }
                unstable {
                    junit 'build/tests/**/TEST-*.xml'
                }
            }
        }
    }
}
