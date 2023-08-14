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
            when {
                expression {
                    params.BASE_VERSION == "ALL" || params.BASE_VERSION in ["11", "10", "9", "8", "7", "3"]
                }
            }
            stages {
                stage('Check license, 2 and 3 in parallel') {
                    parallel {
                        stage ('Check license') {
                            when {
                                expression {
                                    params.BASE_VERSION == "ALL" || params.BASE_VERSION == "11" || params.BASE_VERSION == "10" || params.BASE_VERSION == "9" || params.BASE_VERSION == "8" || params.BASE_VERSION == "7" || params.BASE_VERSION == "3"
                                }
                            }
                            steps {
                                echo "Running Check license steps"
                            }
                        }
                        stage ('Check license 2') {
                            when {
                                expression {
                                    params.BASE_VERSION == "ALL" || params.BASE_VERSION == "11" || params.BASE_VERSION == "10" || params.BASE_VERSION == "9" || params.BASE_VERSION == "8" || params.BASE_VERSION == "7" || params.BASE_VERSION == "3"
                                }
                            }
                            steps {
                                echo "Running Check license 2 steps"
                            }
                        }
                        stage ('Check license 3') {
                            when {
                                expression {
                                    params.BASE_VERSION == "ALL" || params.BASE_VERSION == "11" || params.BASE_VERSION == "10" || params.BASE_VERSION == "9" || params.BASE_VERSION == "8" || params.BASE_VERSION == "7" || params.BASE_VERSION == "3"
                                }
                            }
                            steps {
                                echo "Running Check license 3 steps"
                            }
                        }
                    }
                }
            }
        }
    }    
    post {
        always {
            script {
                if (params.BASE_VERSION == "ALL") {
                    print("Fresh Cluster is not deployed for all versions.")
                } else {
                    print("Fresh Cluster is not deployed for version ${params.BASE_VERSION}.")
                }
            }
        }
    }
}
