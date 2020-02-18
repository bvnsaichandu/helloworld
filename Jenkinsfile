pipeline{
    environment{
        registry = "bvnsaichandu/helloworld"
        registryCredential = '234a8511-2c6b-4c5f-8d8b-57ac8bdf5c02'
        dockerImage = ''
    }
    agent any
    stages{
        stage("git clone"){
            steps{
                git 'https://github.com/bvnsaichandu/helloworld.git'
            }
        }
        stage("Build Test and Package"){
            steps{
                sh 'mvn clean package'
            }
        }
        stage(" Build Docker Image"){
            steps{
                script{
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage(" Deploy to the Docker registry"){
            steps{
                script{
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }    
}
