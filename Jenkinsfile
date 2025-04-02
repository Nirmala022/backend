pipeline {
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        //retry(1)
    }
    environment {
        DEBUG = 'true'
        appVersion = '' //this will become global, we can use across pipeline
    }
    
    stages {
        stage('Read the version') {
            steps {
                script{
                
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "App version: ${appVersion}"
                }
            }   
        }
    }    

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
                
            }
        }
        stage('Docker build') {
            
            steps {
                sh """
                docker build -t joindevops/backend:${appVersion}
                docker images
                """
            }
        }
        stage('Print Params'){
            steps{
                echo "Hello ${params.PERSON}"
                echo "Biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"
                echo "Choice: ${params.CHOICE}"
                echo "Password: ${params.PASSWORD} "
                
            }

        }
    //     stage('Approval') {
    //         input {
    //             message "Should we continue?"
    //             ok "Yes, we should."
    //             submitter "alice,bob"
    //             parameters {
    //                 string(name: 'nirmala', defaultValue: ' default', description: 'Who should I say hello to?')
    //             }
    //         }
    //         steps {
    //             echo "Hello, ${PERSON}, nice to meet you."
    //         }
    //     }    
    // }
    post {
        always{
            echo "this sections runs always"
            deleteDir()
        }
        success{
            echo "this section run when pipeline success"
        }
        failure{
            echo "this dection run when pipeline failure"
        }
    
    }
}