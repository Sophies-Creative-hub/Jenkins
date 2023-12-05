pipeline {
    agent any
    stages {
        stage('One') {
            steps {
                script {
                    writeFile file: 'artifacts/one.txt', text: 'Content for one.txt'
                    echo "Content written to one.txt"
                }
            }
        }

        stage('Two') {
            steps {
                script {
                    echo "Additional stage: Stage Two"
                    sh 'ls -R'  // List all files in the workspace for debugging

                    // Check if one.txt is not empty
                    def isOneTxtEmpty = sh(script: 'test -s artifacts/one.txt', returnStatus: true)
                    
                    if (isOneTxtEmpty == 0) {
                        archiveArtifacts 'artifacts/one.txt'
                    } else {
                        echo "one.txt is empty. Skipping archiving."
                    }
                }
            }
        }

        stage('Three') {
            steps {
                echo "Hello from here"
                archiveArtifacts 'artifacts/three.txt'
            }
        }

        stage('Four') {
            parallel {
                stage('Unit Test') {
                    steps {
                        echo "Running the unit test..."
                        archiveArtifacts 'artifacts/unit_test.txt'
                    }
                }
                stage('Integration test') {
                    steps {
                        echo "Running the integration test..."
                        archiveArtifacts 'artifacts/integration_test.txt'
                    }
                }
            }
        }

        stage('Five') {
            steps {
                echo "Additional stage: Stage Five"
                archiveArtifacts 'artifacts/five.txt'
            }
        }
    }
}
