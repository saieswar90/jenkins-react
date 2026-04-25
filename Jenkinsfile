pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/saieswar90/jenkins-react.git', branch: "${env.BRANCH_NAME}"
            }
        }

        stage('Build and Test') {
            stages {

                stage('Install Dependencies') {
                    steps {
                        bat 'npm install'
                    }
                }

                stage('Run Tests') {
                    steps {
                        bat 'npx vitest run'
                    }
                }

                stage('Build App') {
                    steps {
                        bat 'npm run build'
                    }
                }
            }
        }

        stage('Deployment') {
            when {
                expression { currentBuild.currentResult == 'SUCCESS' }
            }
            stages {

                stage('Deploy to Staging') {
                    when {
                        branch 'development'
                    }
                    steps {
                        echo "🚀 Deploying to STAGING environment"
                    }
                }

                stage('Deploy to Production') {
                    when {
                        branch 'main'
                    }
                    steps {
                        echo "🔥 Deploying to PRODUCTION environment"
                    }
                }
            }
        }
    }
}
