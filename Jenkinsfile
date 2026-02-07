pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven"
    }

    stages {
        stage('Test MVN') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Build MVN') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Deployed on Test ENV') {
            steps {
                echo 'Hello World'
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
