pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    
    environment {
        PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
    }

    stages {
        stage("Build") {
            steps {
                script {
                    // Use 'script' block to wrap multiple shell commands
                    sh 'mvn clean deploy'
                }
            }
        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'valaxy-sonar-scanner'
            }
            steps {
                script {
                    // Use 'script' block to wrap multiple shell commands
                    withSonarQubeEnv('valaxy-sonarqube-server') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}
