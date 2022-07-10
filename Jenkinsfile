pipeline
{
agent any
stages

{ stage ('scm checkout')
 { steps {git branch: 'master', url: 'https://github.com/shirkenitin/maven-project'}         //use pipeline syntax generator to generate script
 }


  stage ('code compile' )
  {steps {  withMaven(globalMavenSettingsConfig: 'c9d791bb-bfbb-414f-8ef9-afbc689969b3', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') 
   { sh 'mvn compile'}
   }}
 
  stage ('code package' )
  {steps {  withMaven(globalMavenSettingsConfig: 'c9d791bb-bfbb-414f-8ef9-afbc689969b3', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') 
   { sh 'mvn clean package'}
   }}
 
 stage ('deployment' )
 {steps{
 sshagent (credentials: ['deploy-dev']) {
    sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@3.69.168.211:/var/lib/tomcat/webapps/'
  }
 }}

 

}
}
