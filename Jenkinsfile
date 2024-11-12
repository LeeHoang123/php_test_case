pipeline {
  agent any
  stages {
    stage ('Checkout Code') {
      steps {
        // Lấy mã nguồn mới nhất từ Git repository
        checkout scm
      }
    }
    stage ('Rebuild and Run Docker Compose') {
      steps {
        // Dừng và xóa container cũ, rồi tái tạo lại container mới với cập nhật code mới
        sh 'sudo docker-compose down'  // Dừng và xóa container cũ
        sh 'sudo docker-compose up -d --build'  // Tái tạo lại container với mã nguồn mới
      }
    }
  }
}



