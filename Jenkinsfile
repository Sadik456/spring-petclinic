pipeline {
    agent any

    triggers {
        cron('H/2 * * * *')
    }

    stages {

        stage('Build & Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('JaCoCo Code Coverage') {
            steps {
                sh 'mvn jacoco:report'
            }
        }

        stage('Package Artifact') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            jacoco execPattern: 'target/jacoco.exec'
        }
    }
}