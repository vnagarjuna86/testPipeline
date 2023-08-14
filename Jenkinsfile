// Pipeline to build a release candidate.
@Library('fwd-jenkins-libraries') _

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
                // Set your variables here
                echo "Running Set variables or other steps"

            }
        }

        stage('Build Jars') {
            steps {
                // Build your jars
                echo "Running Build your jars or other steps"
            }
        }

        stage('Build and Push Containers') {
            steps {
                // Build and push your containers
                echo "Running Build and push your containers or other steps"
            }
        }

        stage('Promote') {
            steps {
                // Perform promotion steps
                echo "Running Perform promotion steps or other steps"
            }
        }

        stage('Build Releases') {
            steps {
                script {
                    if (params.BASE_VERSION == 'ALL') {
                        def baseVersions = ["11", "10", "9", "8", "7", "3"]
                        parallel baseVersions.collectEntries { version ->
                            ["Build $version": {
                                buildRelease(version, params.DEPLOY)
                            }]
                        }
                    } else {
                        buildRelease(params.BASE_VERSION, params.DEPLOY)
                    }
                }
            }
        }

        stage('Functional Test [Others]') {
            steps {
                // Run functional tests or other steps
                echo "Running functional tests or other steps"
            }
        }

        stage('Declarative: Post Actions') {
            steps {
                // Perform post actions
                echo "Running Perform post actions or other steps"
            }
        }
    }
}

def buildRelease(version, deploy) {
    stage("Build Release $version") {
        // Execute the stages for the specified version
        // Fresh Cluster, Check license, Create VMs on AWS, etc.
        if (deploy) {
            // Run stages only if DEPLOY parameter is true
            echo "Building release for version $version"
            // Add your stage executions here

            stage('Fresh Cluster') {
                steps {
                    // Fresh Cluster logic
                    echo "Running Fresh Cluster logic or other steps"
                }
            }

            stage('Check license') {
                steps {
                    // Check license logic
                    echo "Running Check license logic or other steps"
                }
            }

            stage('Create VMs on AWS') {
                steps {
                    // Create VMs logic
                    echo "Running Create VMs logic or other steps"
                }
            }

            stage('Download airgap bundle') {
                steps {
                    // Download airgap bundle
                    echo "Running Download airgap bundle or other steps"
                }
            }

            stage('Install KOTS') {
                steps {
                    // Install KOTS
                    echo "Running Install KOTS or other steps"
                }
            }

            // Add more stages as needed

        } else {
            echo "Not deploying for version $version"
        }
    }
}
