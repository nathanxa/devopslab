pipeline{

    agent any

    stages {

        stage("Git Checkout"){

            steps{

                script{
                    
                    gitCheckout(
                        branch: "main"
                        url: "https://github.com/nathanxa/devopslab.git"
                    )
                                        
                }
            }
        }

    }
}