pipeline{
    agent any
    environment {
        VERSION="${env.VERSION}"
    }

    stages{

        stage('SCM Checkout'){
            steps{
                git 'https://github.com/shirkenitin/maven-project'
               
            }
        }

        stage('code quality check')
        {
            steps
            {
                withSonarQubeEnv(credentialsId: 'Sonar') 
                {
                    
                        sh 'mvn clean package sonar:sonar'
    // some block
                    
                }
            }
        }



    }
}
