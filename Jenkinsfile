pipeline {
    agent any
    stages {
        stage ('Buid Backend') {
            steps {
                   sh 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests'){
            steps {
                sh 'mvn test'
            }
        }
        stage ('Sonar Analysis') {
            enviroment {
                scannerHome = tool 'Sonar_scanner'
            }
            steps {
                withSonarQubeEnv('Sonar_local')
                    sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://192.168.91.155:9000 -Dsonar.login=dbf2fed508bf131a04c380211f25aba01c515710 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/mvn/**,**/src/test/**,**/model/**,**Aplication.java "
            }
        }

        
    }
}



