// Пайплайн раскатки микросервисов (frontend + backend) через Ansible.
// Этап 1: подготовка окружения — установка Docker/Compose и клонирование репозиториев (теги install, clone).
// Этап 2: запуск приложений — запуск микросервисов через docker-compose.yml (тег start).
pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    environment {
        ANSIBLE_DIR  = 'ansible'
        PLAYBOOK     = 'firstPlaybook.yml'
        INVENTORY    = 'inventory/stend1/hosts'
        SSH_CRED_ID  = 'node-ssh-key'
    }

    stages {
        stage('Подготовка окружения') {
            steps {
                dir(env.ANSIBLE_DIR) {
                    ansiblePlaybook(
                        installation: 'ansible',
                        playbook: env.PLAYBOOK,
                        inventory: env.INVENTORY,
                        credentialsId: env.SSH_CRED_ID,
                        tags: 'install,clone',
                        disableHostKeyChecking: true,
                        colorized: true
                    )
                }
            }
        }

        stage('Запуск приложений') {
            steps {
                dir(env.ANSIBLE_DIR) {
                    ansiblePlaybook(
                        installation: 'ansible',
                        playbook: env.PLAYBOOK,
                        inventory: env.INVENTORY,
                        credentialsId: env.SSH_CRED_ID,
                        tags: 'start',
                        disableHostKeyChecking: true,
                        colorized: true
                    )
                }
            }
        }
    }

    post {
        success {
            echo 'Микросервисы развёрнуты и запущены на удалённой ноде.'
        }
        failure {
            echo 'Сборка завершилась с ошибкой, смотрите вывод Ansible выше.'
        }
    }
}
