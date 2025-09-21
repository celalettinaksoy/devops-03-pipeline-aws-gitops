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

        stage("Update the Deployment Tags") {
            steps {
                
                sh """
                   cat deployment.yaml

                   sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g'           deployment.yaml
               
                   cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                   git config --global user.name "mimaraslan"
                   git config --global user.email "mimaraslan@gmail.com"
                   git add deployment.yaml
                   git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                  sh "git push https://github.com/floryos/devops-03-pipeline-aws-gitops main"
                }
            }
        }
    }
}