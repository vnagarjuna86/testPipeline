def myMap = [
    '11': [AMI: 'ami-0f2103a4b8097a560', MASTER_IP: '', WORKER_IPS: 'WORKER_IPS_11', VER: '11'],
    '10': [AMI: 'ami-07c628e683bb46bf3', MASTER_IP: '', WORKER_IPS: 'WORKER_IPS_10', VER: '10']
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
                                AMI_ID = myMap[BASE_VERSION].AMI
                                echo "Running Perform promotion steps or other steps ${BASE_VERSION}"
                                echo "Fetching AMI for Version ${params.BASE_VERSION}: ${AMI_ID}"
                                myMap[BASE_VERSION].MASTER_IP = sh(script: 'echo "192.168.1.${baseVersion}"', returnStdout: true).trim()
                                sh '''
                                    pwd
                                    # echo "Using AMI_ID in shell: \$AMI_ID"
                                    echo "Using AMI_ID in shell: $AMI_ID"
                                    echo "Using MASTER_IP in shell: ${myMap[BASE_VERSION].MASTER_IP}"
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
                            env.AMI_ID = myMap[BASE_VERSION].AMI
                            echo "Running Perform promotion steps or other steps ${BASE_VERSION}"
                            echo "Fetching AMI for Version ${params.BASE_VERSION}: ${AMI_ID}"
                            env.AMI_ID = amiId
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
