pipeline {
    agent any

    tools {
        maven "MAVEN_HOME"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/andromotech/java-tomcat-maven-example.git'
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                
                success {
                    deploy adapters: [tomcat9(credentialsId: 'daf49adc-da8e-4582-9d9b-d5373dc1ffd8', path: '', url: 'http://localhost:8081')], contextPath: null, war: 'target/java-tomcat-maven-example.war'
                }
                always {
                    emailext body: 'Build Status Summary ', subject: '[PROD]Build Status', to: 'adromo.co@gmail.com'
                }
            }
        }
    }
}

