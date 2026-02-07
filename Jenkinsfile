pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
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
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcat-test', path: '', url: 'http://192.168.122.204:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
        stage('Input from Admin') {
            steps {
                Input {
                      message "Should we continue?"
                ok "Yes, we should."
                }
            }
        }
        stage('Deployed on Production ENV') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
