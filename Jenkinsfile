pipeline {
    agent any
    stages {
        stage ('Buid Backend') {
            steps {
                   sh 'mvn clean package -DskipTests=true'
            }
        }
    }
}