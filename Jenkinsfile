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
                sh '''
                # Останавливаем предыдущее приложение, если оно работает
                pkill -f /home/jenkins/agent/deployed-app.jar || true

                # Запускаем приложение в фоновом режиме с логами
                nohup java -jar /home/jenkins/agent/deployed-app.jar > /home/jenkins/agent/app.log 2>&1 &

                # Следим за логами
                tail -f /home/jenkins/agent/app.log &
                '''
            }
        }
    }
}
