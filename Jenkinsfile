pipeline {
    agent any
    environment {
        PATH = "C:\\Users\\Raymond\\AppData\\Local\\Programs\\Python\\Python312;C:\\Users\\Raymond\\AppData\\Local\\Programs\\Python\\Python312\\Scripts;C:\\Program Files\\nodejs;C:\\Users\\Raymond\\AppData\\Roaming\\npm;${env.PATH}"
        HOME = "C:\\Users\\Raymond"
    }

    stages {
        stage('install-pip-deps') {
            steps {
                script{

                    build()
                }
            }
        }

        stage('deploy-to-dev') {
            steps {
                script{
                    deploy("dev", 7001)
                }
            }
        }


        stage('tests-on-dev') {
            steps {
                script{
                    test("dev")
                }
            }
        }

        stage('deploy-to-staging') {
            steps {
                script{
                    deploy("staging", 7002)
                }
            }
        }

        stage('tests-on-staging') {
            steps {
                script{
                    test("staging")
                }
            }
        }

        stage('deploy-to-preprod') {
            steps {
                script{
                    deploy("preprod", 7003)
                }
            }
        }

        stage('tests-on-preprod') {
            steps {
                script{
                    test("preprod")
                }
            }
        }

        stage('deploy-to-prod') {
            steps {
                script{
                    deploy("prod", 7004)
                }
            }
        }

        stage('tests-on-prod') {
            steps {
                script{
                    test("prod")
                }
            }
        }
    }
}


def build(){
    echo 'Cloning repository and installing dependencies...'
    bat 'git clone https://github.com/Raimis01/python-greetings'
    dir('python-greetings') {
        bat 'dir'
        bat 'pip3 install -r requirements.txt'
    }
}
def deploy(String env, int port){
    echo "Start to deploy to ${env}"
    dir('python-greetings') {
        bat "pm2 delete greetings-app-${env} || EXIT /B 0"
        bat "pm2 start app.py --name greetings-app-${env} -- -port ${port}"
    }
}
def test(String env){
    echo "Starting tests on ${env} environment."
    bat 'git clone https://github.com/mtararujs/course-js-api-framework'
    dir('course-js-api-framework') {
        bat 'npm install'
        bat "set NODE_ENV=greetings_${env} && npm run greetings greetings_${env}"
    }
}