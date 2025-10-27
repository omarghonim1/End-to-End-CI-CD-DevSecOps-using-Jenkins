pipeline {
    agent any

    tools {
        jdk 'jdk11'
        maven 'maven3'
    }
    Environment {
        SCANNER_HOME= tool 'sonnar-scanner'
    }

    stages {
        stage('Git COMPILE') {
            steps {
                sh 'mvn clean compile -DskipTests=true'
            }
        }
        stage('OWASP Scan') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --format XML --format HTML', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }    
        stage('Sonarqube') {
            steps {
                withSonarQubeEnv('sonnar-server') {
                   sh '''
                $SCANNER-HOME/bin/sonar-scanner \
                -Dsonar.projectName=Shopping-Cart \
                -Dsonar.java.binaries=. \
                -Dsonar.projectKey=Shopping-Cart
                '''
                }
            }
        }                    
    }
}
