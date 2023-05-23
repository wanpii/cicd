pipeline {
    agent any
    
    stages {
        stage('install-pip-deps') {
            steps {
                echo 'Installing all required dependencies..'
                git url: 'https://github.com/mtararujs/python-greetings.git', branch: 'main'
                bash 'ls'
                sh 'pip3 install -r requirements.txt'
            }
        }
        
        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to dev...'
                deploy('dev', 7001)
            }
        }
        
        stage('tests-on-dev') {
            steps {
                echo 'Running tests on dev...'
                test('dev')
            }
        }
        
        stage('deploy-to-staging') {
            steps {
                echo 'Deploying to staging...'
                deploy('staging', 7002)
            }
        }
        
        stage('tests-on-staging') {
            steps {
                echo 'Running tests on staging...'
                test('staging')
            }
        }
        
        stage('deploy-to-preprod') {
            steps {
                echo 'Deploying to preprod...'
                deploy('preprod', 7003)
            }
        }
        
        stage('tests-on-preprod') {
            steps {
                echo 'Running tests on preprod...'
                test('preprod')
            }
        }
        
        stage('deploy-to-prod') {
            steps {
                echo 'Deploying to prod...'
                deploy('prod', 7004)
            }
        }
        
        stage('tests-on-prod') {
            steps {
                echo 'Running tests on prod...'
                test('prod')
            }
        }
    }
}

def deploy(environment, port) {
    git url: 'https://github.com/mtararujs/python-greetings.git', branch: 'main'
    sh "pm2 delete greetings-app-${environment} & set 'errorlevel=0'"
    sh "pm2 start app.py --name greetings-app-${environment} -- --port ${port}"
}

def test(environment) {
    git url: 'https://github.com/mtararujs/course-js-api-framework.git', branch: 'main'
    sh 'npm install'
    sh "npm run greetings greetings_${environment}"
}
