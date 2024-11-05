// pipeline {
//   agent any
//   stages {
//     stage ('Run Docker Compose') {
//       steps{
//         sh 'sudo docker-compose up -d'
//       }
//     }
//   }
// }

pipeline {
    agent any
    
    triggers {
        pollSCM('* * * * *') // Kiểm tra mã nguồn mỗi phút
    }
    
    environment {
        DOCKER_COMPOSE_FILE = 'docker-compose.yml'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Lấy mã nguồn mới nhất từ Git
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Dừng container cũ (nếu có)
                    sh 'docker-compose -f $DOCKER_COMPOSE_FILE down || true'
                    
                    // Xây dựng container mới
                    sh 'docker-compose -f $DOCKER_COMPOSE_FILE build'
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                // Khởi động container mới ở chế độ nền
                sh 'docker-compose -f $DOCKER_COMPOSE_FILE up -d'
            }
        }
    }
    
    post {
        success {
            echo 'Build và khởi động container mới thành công!'
        }
        failure {
            echo 'Build thất bại. Vui lòng kiểm tra lại!'
        }
    }
}

