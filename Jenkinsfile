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
            if (params.BASE_VERSION != "ALL") {
            /*when {
                expression {
                    params.BASE_VERSION == "ALL" 
                }
            }*/
                matrix {
                    axes {
                        axis {
                            name 'BASE_VERSION'
                            values '11', '10', '9', '8', '7', '3'
                        }
                    }
                    stages {
                        stage ('Check license') {
                            steps {
                                echo "Running Perform promotion steps or other steps ${BASE_VERSION}"
                            }
                        }
                        stage ('Check license 2') {
                            steps {
                                echo "Running Check license 2 or other steps ${BASE_VERSION}"
                            }
                        }
                        stage ('Check license 3') {
                            steps {
                                echo "Running Check license 3 or other steps ${BASE_VERSION}"
                            }
                        }
                    }
                }
            }
            else {
                execute stage('Skip matrix') {
                    steps {
                        echo "Running Skip matrix or other steps ${BASE_VERSION}"
                    }
                }
           } 
    }

    post {
        always {
            script {
                if (params.BASE_VERSION == "ALL") {
                    print("Fresh Cluster is deployed for all versions.")
                } else {
                    print("Fresh Cluster is deployed for version ${params.BASE_VERSION}.")
                }
            }
        }
    }
}
