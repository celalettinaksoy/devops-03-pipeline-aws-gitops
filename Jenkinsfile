pipeline {
    agent {
        label 'Jenkins-Agent'
    }

    environment {
        APP_NAME = "devops-03-pipeline-aws-gitops"
    }

    stages {
        // 1. AŞAMA: WORKSPACE TEMİZLİĞİ
        stage('Cleanup Workspace') {
            steps {
                // Mevcut dizindeki her şeyi siler
                deleteDir()
            }
        }

        // 2. AŞAMA: KODU GITHUB'DAN ÇEKME
        stage('SCM GitHub') {
            steps {
                script {
                    sh "echo 'STAGE BAŞLIYOR: SCM GitHub ✅'"
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/celalettinaksoy/devops-03-pipeline-aws-gitops']])
                    sh "echo 'STAGE TAMAMLANDI: SCM GitHub 🎉'"
                }
            }
        }
        // ... diğer stage'leriniz ...
    }
}