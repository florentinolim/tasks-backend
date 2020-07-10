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
    }
}