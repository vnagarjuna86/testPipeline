def amiMap = [
    '11': 'ami-0f2103a4b8097a570',
    '10': 'ami-07c628e683bb46bh3',
    '9': 'ami-0d40cc67849b82659',
    '8': 'ami-0d4a0d68ad7ea87d2',
    '7': 'ami-0a45b299774e0b2bc',
    '3': 'ami-0a45b299994e0b8bc'
]

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
                    stage ('Check license') {
                        steps {
                            script {
                                env.AMI_ID = amiMap[BASE_VERSION]
                                echo "Running Perform promotion steps or other steps ${BASE_VERSION}"
                                echo "Fetching AMI for Version ${params.BASE_VERSION}: ${AMI_ID}"
                                def baseVersion = BASE_VERSION
                                // Simulate getting the master IP using a shell command
                                def masterIP = sh(script: 'echo "192.168.1.${baseVersion}"', returnStdout: true).trim()
                                masterIPs[baseVersion] = masterIP // Store the master IP in the map
                                echo "Master IP for base version ${baseVersion}: ${masterIP}"
                                sh '''
                                    pwd
                                    # echo "Using AMI_ID in shell: \$AMI_ID"
                                    echo "Using AMI_ID in shell: $AMI_ID"
                                '''
                            }
                        }
                    }
                    stage ('Check license 2') {
                        steps {
                            echo "Running Check license 2 or other steps ${BASE_VERSION}"
                            // def baseVersion = BASE_VERSION
                            def masterIP = masterIPs[BASE_VERSION] // Retrieve the stored master IP
                            // Use the master IP in a 'sh' block
                            sh '''
                                echo "Using IP for base version ${BASE_VERSION}: ${masterIP}"
                                # Add more shell commands that use the master IP
                            '''
                            
                            // Use the master IP in 'steps' block
                            echo "Using IP for base version ${BASE_VERSION}: ${masterIP}"
                            
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
                stage ('Check license') {
                    steps {
                        script {
                            env.AMI_ID = amiMap[BASE_VERSION]
                            echo "Running Perform promotion steps or other steps ${BASE_VERSION}"
                            echo "Fetching AMI for Version ${params.BASE_VERSION}: ${AMI_ID}"
                            sh '''
                                pwd
                                # echo "Using AMI_ID in shell: \$AMI_ID"
                                echo "Using AMI_ID in shell: $AMI_ID"
                            '''
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
