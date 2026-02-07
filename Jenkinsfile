pipeline {
    agent any

    tools {
        maven "Maven"
    }

    stages {

        stage('Test MVN') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build MVN') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deployed on Test ENV') {
            steps {
                deploy adapters: [
                    tomcat9(
                        alternativeDeploymentContext: '',
                        credentialsId: 'Tomcat-test',
                        path: '',
                        url: 'http://192.168.122.204:8080'
                    )
                ],
                contextPath: '/app',
                war: '**/*.war'
            }

            post {
                success {
                    emailext(
                        subject: "✅ Test Deployment SUCCESS - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: """
                        Test Environment Deployment Completed Successfully.
                        Waiting for approval to deploy to PRODUCTION.

                        Job: ${env.JOB_NAME}
                        Build: ${env.BUILD_NUMBER}
                        URL: ${env.BUILD_URL}
                        """,
                        to: "maxmizan33@gmail.com"
                    )
                }

                failure {
                    emailext(
                        subject: "❌ Test Deployment FAILED - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: """
                        Test Deployment FAILED.

                        Job: ${env.JOB_NAME}
                        Build: ${env.BUILD_NUMBER}
                        Console Log:
                        ${env.BUILD_URL}
                        """,
                        to: "maxmizan33@gmail.com"
                    )
                }
            }
        }

        stage('Deployed on Production ENV') {
            steps {
                input message: 'Do you want to deploy to Production?', ok: 'Deploy'

                deploy adapters: [
                    tomcat9(
                        alternativeDeploymentContext: '',
                        credentialsId: 'Tomcat-test',
                        path: '',
                        url: 'http://192.168.122.205:8080'
                    )
                ],
                contextPath: '/app',
                war: '**/*.war'
            }
        }
    }
}
