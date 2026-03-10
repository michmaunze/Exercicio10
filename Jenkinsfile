pipeline {
    agent any

    stages {
        stage('Deploy via SSH') {
            steps {
                withCredentials([
                    string(credentialsId: 'sisd_ip',   variable: 'SERVER_IP'),
                    string(credentialsId: 'sisd_port', variable: 'SERVER_PORT'),
                    string(credentialsId: 'sisd_user', variable: 'SERVER_USER')
                ]) {
                    sshagent(credentials: ['jenkins_key']) {
                        sh '''
                            ssh -o StrictHostKeyChecking=no \
                                -p $SERVER_PORT \
                                $SERVER_USER@$SERVER_IP \
                                'bash /home/michela/cicd.sh'
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Deploy concluído com sucesso!"
        }
        failure {
            echo "Erro no deploy."
        }
    }
}
