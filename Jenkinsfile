pipeline {
    agent any
    triggers {
        pollSCM('*/10 * * * *') // Проверка изменений каждые 10 секунд
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }
    }
}

