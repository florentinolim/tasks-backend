pipeline {
    agent any
{
def mvn_version = ''
    
withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ) 
  {   
      sh  'mvn clean package'
  }

}
    stages {
        stage ('Buid Backend') {
            steps {
                   sh 'mvn clean package -DskipTests=true'
            }
        }
    }
}