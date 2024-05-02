pipeline {
    agent any

    environment {
        REPO_URL_PYTHON = "https://github.com/mtararujs/python-greetings"
        REPO_URL_JS = "https://github.com/mtararujs/course-js-api-framework"
    }

    stages {
        stage('Install pip dependencies') {
            steps {
                script {
                    cloneRepository(env.REPO_URL_PYTHON)
                    bat "dir"
                    bat "pip install -r requirements.txt"
                }
            }
        }

        stage('Deploy to DEV') {
            steps {
                script {
                    deployApp('dev', 7001)
                }
            }
        }
        stage('Tests on DEV') {
            steps {
                script {
                    runTests('dev')
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    deployApp('staging', 7002)
                }
            }
        }
        stage('Tests on Staging') {
            steps {
                script {
                    runTests('staging')
                }
            }
        }

        stage('Deploy to PreProd') {
            steps {
                script {
                    deployApp('preprod', 7003)
                }
            }
        }
        stage('Tests on PreProd') {
            steps {
                script {
                    runTests('preprod')
                }
            }
        }

        stage('Deploy to Prod') {
            steps {
                script {
                    deployApp('prod', 7004)
                }
            }
        }
        stage('Tests on Prod') {
            steps {
                script {
                    runTests('prod')
                }
            }
        }
    }
}

def cloneRepository(String repoUrl) {
    echo "Cloning repository from ${repoUrl}"
    bat "git clone ${repoUrl}"
}

def installDeps() {
    echo 'Installing dependencies'
    bat "npm install"
}

def deployApp(String env, int port) {
    echo "Deploying to ${env} environment on port ${port}"
    bat "pm2 delete greetings-app-${env} || exit 0"
    bat "pm2 start app.py --name greetings-app-${env} -- --port ${port}"
}

def runTests(String env) {
    echo "Running tests on ${env} environment"
    cloneRepository(env.REPO_URL_JS)
    installDeps()
    bat "npm run greetings greetings_${env}"
}
