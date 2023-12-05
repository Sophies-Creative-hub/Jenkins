pipeline {
    agent any
    stages {
        stage('One') {
            steps {
                script {
                    echo "Hi from GitHub" 
                    sh 'ls -R'  // List all files in the workspace for debugging
                }
                script {
                    sh 'echo "Content for one.txt" > artifacts/one.txt'
                    echo "Content written to one.txt"
                    sh 'ls -R'  // List all files in the workspace for debugging
                    sh 'cat artifacts/one.txt'  // Display the content for verification
                }
                archiveArtifacts "artifacts/one.txt"
            }
        }

        stage('Two') {
            steps {
                input message: 'Do you want to proceed?', ok: 'Yes'
                archiveArtifacts 'artifacts/two.txt'
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
