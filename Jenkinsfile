pipeline {
    agent any

    environment {
        versionTags = "" // Initialize versionTags as an empty string to avoid issues with undefined variables
    }

    stages {
        stage('Checkout') {
            steps {
                // Use the "GIT_CRED" credentials to access the private repo
                checkout([$class: 'GitSCM',
                    branches: [[name: "$BRANCH_NAME"]],
                    userRemoteConfigs: [[
                        url: 'https://github.com/akshaysharma25/akshayprod.git',
                        credentialsId: 'GIT_CRED'
                    ]]
                ])
            }
        }
        
        stage('Building Docker Image'){
        	steps {
        		sh 	'''
                    akshay=$(cat test | awk '{$1=$1};1' | sed '/^$/d' | tail -1 | tr -d '\r\n')
                    echo "value of var is = $akshay"
        			docker build . -f devops/Dockerfile -t appimg:akshay-"$akshay"
                    '''
            }
        }
    }

    post {
        always {
            cleanWs() // Clean workspace at the end, regardless of pipeline status
        }
    }
}
