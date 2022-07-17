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
        
         stage('Build Image')
        {
            steps{
                sh 'docker build -t shirkenitin100/tomcat:V1 .'
            }
        }
        stage('Push Image in DockerHub')
        {
        steps{
           withDockerRegistry(credentialsId: 'DockerHub', url: 'https://index.docker.io/v1/') {
    // some block

            
              sh "docker push shirkenitin100/tomcat:V1"
           }   
        }
        }

          stage('Create Docker Container')
        {
        steps{
          
             sh 'docker run -itd -p 24000:8080 shirkenitin100/tomcat:V1'
            
              
           }   
        }
        


        
 }
}
