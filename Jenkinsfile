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
            matrix {
                axes {
                    axis {
                        name 'BASE_VERSION'
                        values 'ALL', '11', '10', '9', '8', '7', '3'
                    }
                }
                stages {
                    stage('Check license') {
                        steps {
                            script {
                                if (params.BASE_VERSION == 'ALL') {
                                    echo "Running Perform promotion steps for all versions."
                                } else {
                                    echo "Running Perform promotion steps for version ${params.BASE_VERSION}."
                                }
                            }
                        }
                    }
                    stage('Check license 2') {
                        steps {
                            script {
                                if (params.BASE_VERSION == 'ALL') {
                                    echo "Running Check license 2 steps for all versions."
                                } else {
                                    echo "Running Check license 2 steps for version ${params.BASE_VERSION}."
                                }
                            }
                        }
                    }
                    stage('Check license 3') {
                        steps {
                            script {
                                if (params.BASE_VERSION == 'ALL') {
                                    echo "Running Check license 3 steps for all versions."
                                } else {
                                    echo "Running Check license 3 steps for version ${params.BASE_VERSION}."
                                }
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
                if (params.BASE_VERSION == 'ALL') {
                    println("Fresh Cluster is deployed for all versions.")
                } else {
                    println("Fresh Cluster is deployed for version ${params.BASE_VERSION}.")
                }
            }
        }
    }
}
