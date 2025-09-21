
pipeline {
    // Pipeline'ın çalışacağı Jenkins agent'ını etiketine göre seçiyoruz.
    agent {
        label 'Jenkins-Agent'
    }
    // Pipeline boyunca geçerli olacak ortam değişkenlerini ayarlıyoruz.
    environment {
        APP_NAME = "devops-03-pipeline-aws-gitops"
    }
    stages {
        // 0. WORKSPACE TEMİZLİĞİ: Her build öncesi Jenkins workspace'ini temizler.
        stage('Cleanup Workspace') {
            steps {
                script {
                    cleanws()
                }
            }
        }
        
        // 1. KODU GITHUB'DAN ÇEKME: Projenin en güncel kodunu 'main' branch'inden çeker.
        stage('SCM GitHub') {
            steps {
                script {
                    sh """
                        echo 'STAGE BAŞLIYOR: SCM GitHub ✅'
                    """
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/celalettinaksoy/devops-03-pipeline-aws-gitops']])
                    sh """
                        echo 'STAGE TAMAMLANDI: SCM GitHub 🎉'
                    """
                }
            }
        }
    }
}    
