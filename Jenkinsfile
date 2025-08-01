pipeline {
    agent any    environment {
        MAVEN_HOME = tool 'Maven 3.8'
        SONARQUBE = 'SonarQube'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/jagan402/java-repo.git', branch: 'main'
            }
        }

        stage('Build & Unit Test') {
            steps {
                sh "${MAVEN_HOME}/bin/mvn clean test"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    sh "${MAVEN_HOME}/bin/mvn sonar:sonar"
                }
            }
        }

        stage('Deploy to Nexus') {
            when {
                branch 'main'
            }
            steps {
                sh "${MAVEN_HOME}/bin/mvn deploy"
            }
        }
    }

    post {
        always {
            echo "Pipeline finished: ${currentBuild.currentResult}"
        }
    }
}
