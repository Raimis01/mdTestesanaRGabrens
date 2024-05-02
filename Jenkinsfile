pipeline {
    agent any
    environment {

        PATH = "C:\\Users\\Raymond\\AppData\\Local\\Programs\\Python\\Python312;C:\\Users\\Raymond\\AppData\\Local\\Programs\\Python\\Python312\\Scripts;C:\\Program Files\\nodejs;C:\\Users\\Raymond\\AppData\\Roaming\\npm;${env.PATH}"
        HOME = "C:\\Users\\Raymond"
    
    }

    stages {
        stage('install-pip-deps') {
            steps {

                build()
            }
        }

        stage('deploy-to-dev') {
            steps {
                deploy("dev", 7001)
            }
        }


        stage('tests-on-dev') {
            steps {
                test("dev")
            }
        }

        // stage('deploy-to-staging') {
        //     steps {
        //         echo 'Deploying to staging environment...'
        //         bat 'pm2 delete greetings-app-staging || EXIT /B 0'
        //         bat 'pm2 start C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\mdTestesana\\python-greetings\\app.py --name greetings-app-staging -- --port 7002'
        //     }
        // }

        // stage('tests-on-staging') {
        //     steps {
        //         echo 'Running tests on staging environment...'
        //         bat 'git clone https://github.com/Raimis01/course-js-api-framework'
        //         dir('course-js-api-framework') {
        //             bat 'npm install'
        //             bat 'npm run greetings greetings_staging'
        //         }
        //     }
        // }

        // stage('deploy-to-preprod') {
        //     steps {
        //         echo 'Deploying to pre-production environment...'
        //         bat 'pm2 delete greetings-app-preprod || EXIT /B 0'
        //         bat 'pm2 start C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\mdTestesana\\python-greetings\\app.py --name greetings-app-preprod -- --port 7003'
        //     }
        // }

        // stage('tests-on-preprod') {
        //     steps {
        //         echo 'Running tests on pre-production environment...'
        //         bat 'git clone https://github.com/Raimis01/course-js-api-framework'
        //         dir('course-js-api-framework') {
        //             bat 'npm install'
        //             bat 'npm run greetings greetings_preprod'
        //         }
        //     }
        // }

        // stage('deploy-to-prod') {
        //     steps {
        //         echo 'Deploying to production environment...'
        //         bat 'pm2 delete greetings-app-prod || EXIT /B 0'
        //         bat 'pm2 start C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\mdTestesana\\python-greetings\\app.py --name greetings-app-prod -- --port 7004'
        //     }
        // }

        // stage('tests-on-prod') {
        //     steps {
        //         echo 'Running tests on production environment...'
        //         bat 'git clone https://github.com/Raimis01/course-js-api-framework'
        //         dir('course-js-api-framework') {
        //             bat 'npm install'
        //             bat 'npm run greetings greetings_prod'
        //         }
        //     }
        // }
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
    bat "pm2 delete greetings-app-\"${env}\" || EXIT /B 0"
    bat "pm2 start app.py --name greetings-app-\"${env}\" --port \"${port}\""

}
def test(String env){
    echo "Starting tests on ${env} environment."
    bat 'git clone https://github.com/mtararujs/course-js-api-framework'
    dir('course-js-api-framework') {
        bat 'npm install'
        bat "set NODE_ENV=greetings_${env} && npm run greetings greetings_${env}"
    }
}