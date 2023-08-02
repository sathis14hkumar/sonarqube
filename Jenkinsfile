pipeline {
    agent any

    tools {
        maven "maven"
        jdk "jdk11"
    }

    stages {
        stage('Initialize') {
            steps {
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }
        stage('Build') {
            steps {
                dir("/var/lib/jenkins/workspace/New_demo/my-app") {
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
}
