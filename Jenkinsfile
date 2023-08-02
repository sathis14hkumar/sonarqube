pipeline {
    agent any

    
        stage('Build') {
            steps {
                dir("/var/lib/jenkins/workspace/son/src") {
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'sonarqube-scanner'
                    withSonarQubeEnv('SonarQubeServer') {
                        dir("/var/lib/jenkins/workspace/son/src") {
                            sh "${scannerHome}/bin/sonar-scanner"
                        }
                    }
                }
            }
        }
    }

    post {
        always {
            junit(
                allowEmptyResults: true,
                testResults: '*/test-reports/*.xml'
            )
        }
    }

