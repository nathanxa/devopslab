@Library('my_shared_lib') _

pipeline{

    agent any

    stages {

        stage("Git Checkout"){

            steps{

                script{
                    gitCheckout(
                        branch: "main"
                        url: "https://github.com/nathanxa/devopslab_java_app.git"
                    )
                }
            }
        }

    }
}