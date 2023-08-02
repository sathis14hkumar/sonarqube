pipeline {
    agent any
        
    stages {
       
    
       
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'sonarqube'
                    withSonarQubeEnv('sonarqube') {
                        dir("/var/lib/jenkins/workspace/son/src") {
                            sh "${scannerHome}/bin/sonar-scanner"
                        }
                    }
                }
            }
        }
    }

    
}
