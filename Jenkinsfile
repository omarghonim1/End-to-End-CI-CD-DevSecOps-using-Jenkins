pipeline {
    agent any

    tools {
        jdk 'jdk11'
        maven 'maven3'
    }

    stages {
        stage('Git COMPILE') {
            steps {
                sh 'mvn clean compile -DskipTests=true'
            }
        }
    }
}
