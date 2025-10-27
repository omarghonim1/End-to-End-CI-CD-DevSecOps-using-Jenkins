pipeline {
    agent any

    tools {
        jdk 'jdk11'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
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
        stage('SonarQube') {
            steps {
                withSonarQubeEnv('sonar-server') {
                   sh '''
                $SCANNER_HOME/bin/sonar-scanner \
                -Dsonar.projectName=Shopping-Cart \
                -Dsonar.java.binaries=. \
                -Dsonar.projectKey=Shopping-Cart
                '''
                }
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests=true"     
            }
        }   
        stage('Docker Build & Push') {
            steps {
                withDockerRegistry(credentialsId: '1ab8a8fa-fdeb-4e36-8bc7-43b7c3ef30f4', url: 'https://index.docker.io/v1/') {
                    sh "docker build -t shopping-cart -f docker/Dockerfile ."
                    sh "docker tag shopping-cart omarghonim/shopping-cart:latest"
                    sh "docker push omarghonim/shopping-cart:latest"
                }     
            }
        }
        stage('Deploy') {
            steps {
                script {
                withDockerRegistry(credentialsId: '1ab8a8fa-fdeb-4e36-8bc7-43b7c3ef30f4', url: 'https://index.docker.io/v1/') {
                sh ''' 
                    docker run -d --name merch-shop \
                    --ulimit nofile=65535:65535 \
                    -p 8070:8080 \
                    -e JAVA_OPTS="-Xms256m -Xmx1024m -Djava.security.egd=file:/dev/./urandom -Djava.io.tmpdir=/tmp" \
                    omarghonim/shopping-cart:latest
                '''
                    }
                }
            }
        }                                           
    }
}
