pipeline {
    agent any

    parameters {
        choice(
            name: 'BASE_VERSION',
            choices: ["ALL", "11", "10", "9", "8", "7", "3"],
            description: 'Select base version(s) to trigger'
        )
        booleanParam(
            name: 'DEPLOY',
            defaultValue: true,
            description: 'Deploy fresh cluster'
        )
    }

    stages {
        stage('Set variables') {
            steps {
                echo "Running Set variables or other steps"
            }
        }

        stage('Build Jars') {
            steps {
                echo "Running Build your jars or other steps"
            }
        }

        stage('Build and Push Containers') {
            steps {
                echo "Running Build and push your containers or other steps"
            }
        }

        stage('Promote') {
            steps {
                echo "Running Perform promotion steps or other steps"
            }
        }

        stage('Fresh Cluster') {
            stages {
                    stage ('Check license') {
                        steps {
                            echo "Running Perform promotion steps or other steps"
                        }
                    }
                    stage ('Check license 2') {
                        steps {
                            echo "Running Check license 2 or other steps"
                        }
                    }
                    stage ('Check license 3') {
                        steps {
                            echo "Running Check license 3 or other steps"
                        }
                    }
            }
        }
    }    
    post {
    always {
        script {
            print ("Fresh Cluster is not deployed.")
            }
        }
    }
}
