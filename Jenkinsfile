pipeline {
    agent any
    environment {
        // 定义环境变量
        APP_NAME = "my_application"
    }
    stages {
        stage('Checkout') {
            steps {
                // 检出代码
                echo "检出代码"
            }
        }
        stage('Build') {
            steps {
                // 构建项目，这里以 Maven 项目为例
                echo "构建项目${env.BRANCH_NAME}"
            }
        }

        stage('Deploy-PROD') {
            when {
                // 仅在特定分支部署
                branch 'master'
            }
            steps {
                // 部署到生产环境，这里用模拟脚本代替
                echo "部署master"
            }
        }
        stage('Deploy-UAT') {
            when {
                // 仅在特定分支部署
                branch 'uat'
            }
            steps {
                // 部署到生产环境，这里用模拟脚本代替
                echo "部署dev/v1.0.1"
            }
        }
    }
    post {
        always {
            // 无论构建结果如何，都执行清理工作
            cleanWs()
        }
        success {
            // 构建成功时发送通知
           // emailext subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} succeeded",
            //          body: "The build for branch ${env.BRANCH_NAME} has succeeded.",
             //         to: "team@example.com"
             echo "构建成功发送邮件"
        }
        failure {
            // 构建失败时发送通知
           // emailext subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} failed",
           //           body: "The build for branch ${env.BRANCH_NAME} has failed.",
           //           to: "team@example.com"
           echo "构建失败，发送邮件"
        }
    }
}