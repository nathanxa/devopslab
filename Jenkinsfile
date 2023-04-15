@Library('my_shared_lib') _

pipeline{

    agent any

    parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destory')
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

    }
}