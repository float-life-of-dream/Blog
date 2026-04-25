pipeline {
    agent any

    environment {
        PYTHON_VERSION = '3.12'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                            python3 -m venv venv
                            . venv/bin/activate
                            pip install --upgrade pip
                            pip install -r requirements.txt
                        '''
                    } else {
                        bat '''
                            python -m venv venv
                            call venv\\Scripts\\activate.bat
                            pip install --upgrade pip
                            pip install -r requirements.txt
                        '''
                    }
                }
            }
        }

        stage('Build Site') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                            . venv/bin/activate
                            mkdocs build --strict
                        '''
                    } else {
                        bat '''
                            call venv\\Scripts\\activate.bat
                            python -m mkdocs build --strict
                        '''
                    }
                }
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'site/**', fingerprint: true
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                script {
                    currentBuild.result = null

                    // Deploy to GitHub Pages (gh-pages branch)
                    // Requires a Git credential bound as 'github-credentials' in Jenkins
                    if (isUnix()) {
                        withCredentials([usernamePassword(
                            credentialsId: 'github-credentials',
                            usernameVariable: 'GH_USER',
                            passwordVariable: 'GH_TOKEN'
                        )]) {
                            sh '''
                                git config user.name "Jenkins CI"
                                git config user.email "jenkins@ci.local"

                                cp -r site /tmp/site-deploy
                                git checkout gh-pages || git checkout --orphan gh-pages
                                git rm -rf .
                                cp -r /tmp/site-deploy/* .
                                touch .nojekyll

                                git add -A
                                git diff --staged --quiet || git commit -m "Deploy: ${BUILD_TAG} [${BUILD_NUMBER}]"

                                git push https://${GH_TOKEN}@github.com/${GIT_URL##*github.com/} gh-pages
                            '''
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Build #${BUILD_NUMBER} succeeded — site/ is archived."
        }
        failure {
            echo "Build #${BUILD_NUMBER} failed. Check the logs above."
        }
        always {
            cleanWs()
        }
    }
}
