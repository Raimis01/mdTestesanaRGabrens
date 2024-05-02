pipeline {
    agent any
    environment {

        PATH = "C:\\Users\\Raymond\\AppData\\Local\\Programs\\Python\\Python312;C:\\Users\\Raymond\\AppData\\Local\\Programs\\Python\\Python312\\Scripts;C:\\Program Files\\nodejs;C:\\Users\\Raymond\\AppData\\Roaming\\npm;${env.PATH}"
        HOME = "C:\\Users\\Raymond"
    
    }

    stages {
        stage('install-pip-deps') {
            steps {
                echo 'Cloning repository and installing dependencies...'
                bat 'git clone https://github.com/mtararujs/python-greetings'
                dir('python-greetings') {
                    bat 'dir'
                    bat 'pip3 install -r requirements.txt'
                }
            }
        }

        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to development environment...'
                bat 'pm2 delete greetings-app-dev || EXIT /B 0'
                bat 'pm2 start C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\mdTestesana\\python-greetings\\app.py --name greetings-app-dev -- --port 7001'

            }
        }

        stage('tests-on-dev') {
            steps {
                echo 'Running tests on development environment...'
                bat 'git clone https://github.com/Raimis01/course-js-api-framework'
                bat 'npm install'
                bat 'npm run greetings greetings_dev'
            }
        }

        stage('deploy-to-staging') {
            steps {
                echo 'Deploying to staging environment...'
                bat 'pm2 delete greetings-app-staging || EXIT /B 0'
                bat 'pm2 start C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\mdTestesana\\python-greetings\\app.py --name greetings-app-staging -- --port 7002'
            }
        }

        stage('tests-on-staging') {
            steps {
                echo 'Running tests on staging environment...'
                bat 'git clone https://github.com/Raimis01/course-js-api-framework'
                bat 'npm install'
                bat 'npm run greetings greetings_staging'
            }
        }

        stage('deploy-to-preprod') {
            steps {
                echo 'Deploying to pre-production environment...'
                bat 'pm2 delete greetings-app-preprod || EXIT /B 0'
                bat 'pm2 start C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\mdTestesana\\python-greetings\\app.py --name greetings-app-preprod -- --port 7003'
            }
        }

        stage('tests-on-preprod') {
            steps {
                echo 'Running tests on pre-production environment...'
                bat 'git clone https://github.com/Raimis01/course-js-api-framework'
                bat 'npm install'
                bat 'npm run greetings greetings_preprod'
            }
        }

        stage('deploy-to-prod') {
            steps {
                echo 'Deploying to production environment...'
                bat 'pm2 delete greetings-app-prod || EXIT /B 0'
                bat 'pm2 start C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\mdTestesana\\python-greetings\\app.py --name greetings-app-prod -- --port 7004'
            }
        }

        stage('tests-on-prod') {
            steps {
                echo 'Running tests on production environment...'
                bat 'git clone https://github.com/Raimis01/course-js-api-framework'
                bat 'npm install'
                bat 'npm run greetings greetings_prod'
            }
        }
    }
}
