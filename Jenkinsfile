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

        stage('Build Releases') {
            steps {
                script {
                    def baseVersions = params.BASE_VERSION == 'ALL' ?
                                      ["11", "10", "9", "8", "7", "3"] :
                                      [params.BASE_VERSION]

                    parallel baseVersions.collectEntries { version ->
                        def deployForVersion = version == params.BASE_VERSION
                        def stepsForVersion = [
                            "Build Releases (for version $version)": {
                                stage('Fresh Cluster') {
                                    steps {
                                        if (deployForVersion) {
                                            echo "Running Fresh Cluster logic or other steps for version $version"
                                        } else {
                                            echo "Skipping Fresh Cluster for version $version"
                                        }
                                    }
                                }

                                stage('Check license') {
                                    steps {
                                        if (deployForVersion) {
                                            echo "Running Check license logic or other steps for version $version"
                                        } else {
                                            echo "Skipping Check license for version $version"
                                        }
                                    }
                                }

                                stage('Create VMs on AWS') {
                                    steps {
                                        if (deployForVersion) {
                                            echo "Running Create VMs logic or other steps for version $version"
                                        } else {
                                            echo "Skipping Create VMs for version $version"
                                        }
                                    }
                                }

                                stage('Functional Test [Others]') {
                                    steps {
                                        if (deployForVersion) {
                                            echo "Running functional tests or other steps for version $version"
                                        } else {
                                            echo "Skipping functional tests for version $version"
                                        }
                                    }
                                }
                            }
                        ]

                        return [version, stepsForVersion]
                    }
                }
            }
        }

        stage('Declarative: Post Actions') {
            steps {
                echo "Running Perform post actions or other steps"
            }
        }
    }
}
