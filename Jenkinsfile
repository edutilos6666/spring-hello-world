pipeline {
    agent any 
    parameters {
       choice(name: "selectedVersion", choices: ["1.0.0", "1.0.1", "1.1.0"], description: "User chooses the build version")
       booleanParam(name: "executeInit", defaultValue: true, description: "")
    }
    stages {
        stage("init") {
            when {
                expression {
                    params.executeInit
                }
            }
            steps {
                withDockerContainer(image: 'maven',  toolName: 'Docker') {
                    // some block
                    sh 'mvn --version'
                }    
                echo "${env.BRANCH_NAME}"
                echo "${env.BUILD_NUMBER}"
                echo "selectedVersion = ${params.selectedVersion}"
            }
        }
        stage('Compile') {
            steps {
                echo 'Compiling the application!' 
            }
        }
        
        stage("Test"){
            steps {
                echo "Testing the application"
            }
        }
        
        stage("Build") {
            steps {
                echo "Building the application"
            }
        }
        
        stage("Docker Image Create") {
            steps {
               echo "Creating docker image"    
            }
        }
        
        stage("Docker Image Push") {
            steps {
                echo "Pushing docker image to the docker registry"    
            }
            
        }
    }
}
