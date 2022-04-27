pipeline
{
agent any
stages

{ stage ('scm checkout')
 { steps {git branch: 'master', url: 'https://github.com/shirkenitin/maven-project'}         //use pipeline syntax generator to generate script
 }


  stage ('code compile' )
  {steps {  withMaven(globalMavenSettingsConfig: 'dae121f9-58da-4780-89d1-a09462a7df4d', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') 
   { sh 'mvn package'}
   }}
 

 

}
}
