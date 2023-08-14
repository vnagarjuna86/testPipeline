pipeline {
    agent any
    
    parameters {
        choice(name: 'VERSION', choices: ['all', '1', '2', '3', '4', '5'], description: 'Select the version')
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out the repository"
                // Add actual code to checkout your repository here
            }
        }
        
        stage('Build') {
            when {
                expression {
                    params.VERSION == 'all' || params.VERSION == '1'
                }
            }
            steps {
                echo "Building for version ${params.VERSION}"
                // Add actual build steps here
            }
        }
        
        stage('Test') {
            when {
                expression {
                    params.VERSION == 'all' || params.VERSION == '2'
                }
            }
            steps {
                echo "Testing for version ${params.VERSION}"
                // Add actual test steps here
            }
        }
        
        stage('Deploy') {
            when {
                expression {
                    params.VERSION == 'all' || params.VERSION == '3'
                }
            }
            steps {
                echo "Deploying for version ${params.VERSION}"
                // Add actual deployment steps here
            }
        }
        
        stage('Other Stages') {
            when {
                expression {
                    params.VERSION == 'all' || params.VERSION == '4'
                }
            }
            steps {
                echo "Running other stages for version ${params.VERSION}"
                // Add other stages' steps here
            }
        }
        
        stage('Cleanup') {
            when {
                expression {
                    params.VERSION == 'all' || params.VERSION == '5'
                }
            }
            steps {
                echo "Cleaning up for version ${params.VERSION}"
                // Add cleanup steps here
            }
        }
    }
    
    post {
        always {
            echo "Pipeline completed for version ${params.VERSION}"
        }
    }
}
