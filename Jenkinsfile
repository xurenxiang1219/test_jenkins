pipeline {
    agent any
    environment {
        // 定义环境变量
        APP_NAME = "my_application"
    }
    stages {
        stage('Checkout(main)') {
            steps {
                // 检出代码
                echo "检出代码"
                  checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']], // 指定分支
                    userRemoteConfigs: [[
                        url: 'https://SZSystemDeveloper@bitbucket.org/midlanddevelop/mr-lms.git', // 仓库地址
                        credentialsId: 'f598185f-b5ff-44ac-bd1c-a48e5b320d38' // 凭据 ID
                    ]],
                    extensions: [
                        [$class: 'CleanBeforeCheckout'], // 清理工作区
                        [$class: 'SubmoduleOption', recursive: true] // 拉取子模块
                    ]
                ])
                sh 'ls -al'
            }
        }
        stage('Checkout(uat)') {
            steps {
                // 检出代码
                echo "检出代码"
                  checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/uat']], // 指定分支
                    userRemoteConfigs: [[
                        url: 'https://SZSystemDeveloper@bitbucket.org/midlanddevelop/mr-lms.git', // 仓库地址
                        credentialsId: 'f598185f-b5ff-44ac-bd1c-a48e5b320d38' // 凭据 ID
                    ]],
                    extensions: [
                        [$class: 'CleanBeforeCheckout'], // 清理工作区
                        [$class: 'SubmoduleOption', recursive: true] // 拉取子模块
                    ]
                ])
                sh 'ls -al'
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