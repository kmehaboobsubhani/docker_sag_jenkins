
pipeline {
    agent none

    options {
        buildDiscarder(logRotator(numToKeepStr:'10'))
        disableConcurrentBuilds()
    }

    stages {
        stage("Up") {
            agent {
                label 'w64' // this is Windows pipeline
            }
          
            steps {
                unstash 'scripts'
                bat 'ant up -Dcc=internal -Denv=internal'
              
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
