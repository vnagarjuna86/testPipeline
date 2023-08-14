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
                    params.BASE_VERSION == 'ALL' || params.BASE_VERSION in ['11', '10', '9', '8', '7', '3']
                }
            }
            steps {
                script {
                    def versions
                    if (params.BASE_VERSION == 'ALL') {
                        versions = ['11', '10', '9', '8', '7', '3']
                    } else {
                        versions = [params.BASE_VERSION]
                    }

                    for (def version in versions) {
                        echo "Running steps for version ${version}"
                        stage('Check license') {
                            steps {
                                echo "Running Check license steps for version ${version}."
                            }
                        }
                        stage('Check license 2') {
                            steps {
                                echo "Running Check license 2 steps for version ${version}."
                            }
                        }
                        stage('Check license 3') {
                            steps {
                                echo "Running Check license 3 steps for version ${version}."
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
