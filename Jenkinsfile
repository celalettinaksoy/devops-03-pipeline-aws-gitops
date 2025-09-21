pipeline {
    agent {
        label 'Jenkins-Agent'
    }

    environment {
        APP_NAME = "devops-03-pipeline-aws-gitops"
        // DÜZELTME 1: IMAGE_TAG değişkeni build numarası olarak tanımlandı.
        IMAGE_TAG = "${BUILD_NUMBER}" 
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

        stage("Update the Deployment Tags") {
            steps {
                sh """
                    echo "--- deployment.yaml ÖNCE ---"
                    cat deployment.yaml

                    // IMAGE_TAG değişkeni artık Jenkins build numarasını kullanacak
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g'        deployment.yaml
                
                    echo "--- deployment.yaml SONRA ---"
                    cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                    git config --global user.name "celalettinaksoy"
                    git config --global user.email "celalettinaksoy@gmail.com"
                    git add deployment.yaml
                    git commit -m "Updated Deployment Manifest to version ${IMAGE_TAG}"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github-token', gitToolName: 'Default')]) {
                    // DÜZELTME 2: Push yapılan repo adresi checkout yapılanla aynı olacak şekilde düzeltildi.
                    sh "git push https://github.com/celalettinaksoy/devops-03-pipeline-aws-gitops main"
                }
            }
        }
    }
}