pipeline{
    agent any
    environment {
        VERSION="${env.VERSION}"
         registryCredential = 'ecr:eu-central-1:awscreds'
        appRegistry = "081313360202.dkr.ecr.eu-central-1.amazonaws.com/nitin"
        vprofileRegistry = "https://081313360202.dkr.ecr.eu-central-1.amazonaws.com"
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
                withSonarQubeEnv(credentialsId: 'SonarCredentials') {
                    
                        sh 'mvn clean package sonar:sonar'
                     
                    }
            }
        }
    }
        
         stage('Compile')
        {
            steps{
                withMaven(globalMavenSettingsConfig: '6290f137-1930-4d4d-9151-3acc8c921b3b', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') {
                    sh 'mvn compile' 
                }
            }
        }

       stage ('Package' )
        {
            steps {
                  withMaven(globalMavenSettingsConfig: '6290f137-1930-4d4d-9151-3acc8c921b3b', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') {
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
        
        
         stage('Upload Image at ECR') {
          steps{
            script {
              docker.withRegistry( vprofileRegistry, registryCredential ) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
              }
            }
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
