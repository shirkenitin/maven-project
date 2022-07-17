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
                    
                        sh 'mvn clean package sonar:sonar'
                     
                    }
            }
        }
    }
        
         stage('Compile')
        {
            steps{
                withMaven(globalMavenSettingsConfig: 'c9d791bb-bfbb-414f-8ef9-afbc689969b3', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') {
                    sh 'mvn compile' 
                }
            }
        }

       stage ('Package' )
        {
            steps {
                  withMaven(globalMavenSettingsConfig: 'c9d791bb-bfbb-414f-8ef9-afbc689969b3', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') {
                   sh 'mvn clean package'
                }
        }
        }
        
 }
}
