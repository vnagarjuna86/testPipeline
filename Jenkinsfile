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
                        ["Build and Test $version": {
                            buildAndTestRelease(version, params.DEPLOY)
                        }]
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

def buildAndTestRelease(version, deploy) {
    stage("Build and Test Release $version") {
        if (deploy) {
            echo "Building and testing release for version $version"
            
            // Build release stages
            stage('Fresh Cluster') {
                steps {
                    echo "Running Fresh Cluster logic or other steps for version $version"
                }
            }

            stage('Check license') {
                steps {
                    echo "Running Check license logic or other steps for version $version"
                }
            }

            stage('Create VMs on AWS') {
                steps {
                    echo "Running Create VMs logic or other steps for version $version"
                }
            }

            // Add more stages as needed

            // Functional test stage
            stage('Functional Test [Others]') {
                steps {
                    echo "Running functional tests or other steps for version $version"
                }
            }
        } else {
            echo "Not deploying for version $version"
        }
    }
}
