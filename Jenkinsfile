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
            steps{ withMaven(jdk: 'JAVA_HOME', maven: 'MAVEN_HOME')
            {
                withSonarQubeEnv(credentialsId: 'Sonar') 
                {
                    
                        sh 'mvn clean package sonar:sonar'
    // some block
                    
                }
            }}
        }



    }
}
