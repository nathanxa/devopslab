@Library('my_shared_lib') _

pipeline{

    agent any

    parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destory')
        String(name: 'ImageName', description: "name of the docker build", defaultvalue: 'javapp')
        String(name: 'ImageTag', description: "Tag of the docker build", defaultvalue: 'v1')
        String(name: 'AppName', description: "name of the Application", defaultvalue: 'springboot')
    }

    stages {
      
        stage("Git Checkout"){
            when { expression { params.action == 'create'}}

            steps{
            gitCheckout(
                branch: "main",
                url: "https://github.com/nathanxa/devopslab.git"
            )
            }
        }

        stage("Unit Test maven"){
        when { expression { params.action == 'create'}}
            steps{
                script{
                    mvnTest()
                }
            }
        }

        stage("Integration Test maven"){
        when { expression { params.action == 'create'}}
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }

        stage("SCA: SonarQube"){
        when { expression { params.action == 'create'}}
            steps{
                script{
                    def SonarQubecredentialsId = 'sonar-api'
                    staticCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }

        stage("Quality Gate Status Check: SonarQube"){
        when { expression { params.action == 'create'}}
            steps{
                script{
                    def SonarQubecredentialsId = 'sonar-api'
                    qualityGateStatus(SonarQubecredentialsId)
                }
            }
        }

        stage("Maven Build: maven"){
        when { expression { params.action == 'create'}}
            steps{
                script{
                    mvnBuild()
                }
            }
        }

        stage("Docker Build"){
        when { expression { params.action == 'create'}}
            steps{
                script{

                    dockerBuild("${params.ImageName}","${params.ImageTag}","${params.AppName}")
                }
            }
        }

    }
}