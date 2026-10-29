pipeline {
    agent any

    environment {
        DB_URL = 'mysql://user:password@host:3306/db'
        DEPLOY_ENV = 'production'
    }

    stages {
        stage('Сборка') {
            steps {
                echo 'Сборка приложения...'
                echo 'Студент: Пройдаков, вариант: 9'
                sh 'ls -la'
                echo "DB_URL: ${DB_URL}"
                echo "DEPLOY_ENV: ${DEPLOY_ENV}"
                echo "Номер сборки: ${env.BUILD_NUMBER}"
            }
        }
        stage('Тестирование') {
            steps {
                echo 'Тестирование приложения...'
                sh 'chmod +x ./smoke-tests && ./smoke-tests'
            }
        }
        stage('Деплой на staging') {
            steps {
                echo 'Деплой на staging...'
                sh 'chmod +x ./deploy && ./deploy staging'
            }
        }
        stage('Проверка работоспособности') {
            steps {
                echo 'Проверка работоспособности...'
                sh './smoke-tests'
            }
        }
        stage('Деплой на продакшн') {
            steps {
                echo 'Деплой на продакшн...'
                sh './deploy production'
            }
        }
    }

    post {
        always {
            echo 'Это выполняется независимо от статуса завершения'
            script {
                deleteDir()
            }
        }
        success {
            echo 'Сборка успешно завершена'
        }
    }
}