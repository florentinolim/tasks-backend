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
            environment {
                scannerHome = tool 'Sonar_scanner'
            }
            steps {
                withSonarQubeEnv('Sonar_local'){
                    sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://192.168.91.155:9000 -Dsonar.login=dbf2fed508bf131a04c380211f25aba01c515710 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/mvn/**,**/src/test/**,**/model/**,**Aplication.java "
                }
                    
            }
        }
        stage ('Quality Gate') {
            steps {
                sleep(5)
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage ('Deploy Backend'){
            steps {
                deploy adapters: [tomcat8(credentialsId: 'ToncatLogin', path: '', url: 'http://192.168.91.156:8001/')], contextPath: '/tasks-backend', war: 'target/*.war'
            }
        }
        stage ('API Test') {
            steps {
                git credentialsId: 'user', url: 'https://github.com/florentinolim/tasks-api-teste'
                sh 'mvn test'
            }
        }
    }
}



