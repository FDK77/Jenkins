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
                pkill -f /home/jenkins/agent/deployed-app.jar || true
                cp target/HelloJenkins-1.0-SNAPSHOT.jar /home/jenkins/agent/deployed-app.jar
                nohup java -jar /home/jenkins/agent/deployed-app.jar > /home/jenkins/agent/app.log 2>&1 &
                tail -f /home/jenkins/agent/app.log
                '''
            }
        }
    }
}
