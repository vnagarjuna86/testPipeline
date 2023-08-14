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
        stage('Fresh Cluster') {
            when {
                expression {
                    params.BASE_VERSION == "ALL"
                }
            }
            matrix {
                axes {
                    axis {
                        name 'BASE_VERSION'
                        values '11', '10', '9', '8', '7', '3'
                    }
                }
                stages {
                     stage('Fetch AMI') {
                        steps {
                            script {
                                def amiMap = [
                                    '11': 'ami-0f2103a4b8097a560',
                                    '10': 'ami-07c628e683bb46bf3',
                                    '9': 'ami-0d40cc67849b82059',
                                    '8': 'ami-0d4a0d68ad7ea84d2',
                                    '7': 'ami-0a45b299774e0b9bc',
                                    '3': 'ami-0a45b299994e0b9bc'
                                ]
                                def amiId = amiMap[BASE_VERSION]
                                echo "Fetching AMI for Version ${BASE_VERSION}: ${amiId}"
                            }
                        }
                    }
                    stage ('Check license') {
                        steps {
                            script {
                                echo "Running Perform promotion steps or other steps ${BASE_VERSION}"
                                echo "Fetching AMI for Version ${BASE_VERSION}: ${amiId}"
                            }
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
        stage('Desired Version Fresh Cluster') {
            when {
                expression {
                    params.BASE_VERSION != "ALL"
                }
            }
            stages {
                 stage('Fetch AMI') {
                        steps {
                            script {
                                def amiMap = [
                                    '11': 'ami-0f2103a4b8097a560',
                                    '10': 'ami-07c628e683bb46bf3',
                                    '9': 'ami-0d40cc67849b82059',
                                    '8': 'ami-0d4a0d68ad7ea84d2',
                                    '7': 'ami-0a45b299774e0b9bc',
                                    '3': 'ami-0a45b299994e0b9bc'
                                ]
                                def amiId = amiMap[BASE_VERSION]
                                echo "Fetching AMI for Version ${BASE_VERSION}: ${amiId}"
                            }
                        }
                }
                stage ('Check license') {
                    steps {
                        echo "Running Perform promotion steps or other steps ${BASE_VERSION}"
                        // echo "Fetching AMI for Version ${BASE_VERSION}: ${amiId}"
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
