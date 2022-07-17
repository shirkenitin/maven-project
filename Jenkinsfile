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

        stage('code quality check'){
            steps{
                 script{
                withSonarQubeEnv(credentialsId: 'Sonar') {
                     withMaven(maven:'Maven 3.5') {
                        sh 'mvn clean package sonar:sonar'
                     }
}
            }
        }
    }
 }
}
