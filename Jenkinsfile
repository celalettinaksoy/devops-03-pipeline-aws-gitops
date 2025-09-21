pipeline {
    agent {
        label 'Jenkins-Agent'
    }

    // Pipeline seçeneklerini burada tanımlıyoruz
    options {
        // Her build öncesi workspace'i otomatik olarak temizle
        cleanWs() 
    }

    environment {
        APP_NAME = "devops-03-pipeline-aws-gitops"
    }

    stages {
        // ARTIK BU STAGE'E İHTİYAÇ YOK
        // stage('Cleanup Workspace') { ... }

        // 1. KODU GITHUB'DAN ÇEKME
        stage('SCM GitHub') {
            steps {
                script {
                    sh "echo 'STAGE BAŞLIYOR: SCM GitHub ✅'"
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/celalettinaksoy/devops-03-pipeline-aws-gitops']])
                    sh "echo 'STAGE TAMAMLANDI: SCM GitHub 🎉'"
                }
            }
        }
        // ... 
    }
}