@Library('my_shared_lib') _

pipeline{

    agent any

    stages {

        stage("Git Checkout"){

            steps{
            gitCheckout(
                branch: "main",
                url: "https://github.com/nathanxa/devopslab.git"
            )
            }
        }

        stage("Unit Test maven"){

            steps{
                script(

                    mvnTest()
                )
            }
        }
    }
}