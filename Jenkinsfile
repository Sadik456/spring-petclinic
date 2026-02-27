pipeline {
    agent any

    triggers {
        cron('H/5 * * * 4')   // every 5 minutes on Thursday
    }

    stages {
        stage('Build & Test') {
            steps {
                sh 'mvn -v'
                sh 'mvn clean test'
            }
        }

        stage('JaCoCo Coverage Report') {
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
        }
    }
}
