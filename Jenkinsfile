pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // Проверка изменений каждую минуту
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
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Копируем JAR в контейнер агента и запускаем
                sh '''
                cp target/*.jar /home/jenkins/agent/deployed-app.jar
                nohup java -jar /home/jenkins/agent/deployed-app.jar > /home/jenkins/agent/app.log 2>&1 &
                '''
            }
        }
    }
}
