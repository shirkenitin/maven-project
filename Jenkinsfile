pipeline{
    agent any
    environment {
        VERSION="${env.VERSION}"
    }

    stages{

        stage('SCM Checkout'){
            steps{
                git 'https://github.com/shirkenitin/maven-project'
                script {
   sh ' SCM checkout Success'
}
                
            }
        }
    }
 }
