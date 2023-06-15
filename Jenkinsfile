pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                configFileProvider([configFile(fileId: 'bot-config', variable: 'BOT_CONFIG')]) {
                    sh '''
                        source $BOT_CONFIG
                        sed -i "s/your_token/$BOT_TOKEN/" .env
                    '''
                sh 'docker build -t faterek/throw-em .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop throw-em && docker rm throw-em || echo "container does not exist"'
                sh 'docker run --name=throw-em --restart=always -d faterek/throw-em'
                }	
            }
        }
    }
}
