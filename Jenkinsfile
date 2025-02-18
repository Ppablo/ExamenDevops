pipeline {
    agent none

    stages {
        stage('comprobar conexion SHH con servidor digital Ocean') {
            when {
                branch 'jenkins'
            }
            agent any

            steps {
                sshagent(['ssh-key']) {
                    sh 'ssh -o StrictHostKeyChecking=no root@204.48.22.13 "echo conexion correcta"'
                }
            }
        }

        stage('Desplegar node a Digital Ocean') {
            when {
                branch 'jenkins'
            }
            agent any

            steps {
                sshagent(['ssh-key']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no root@204.48.22.13 "
                        cd ~/codigo/pablogiraldo/ &&
                        rm -rf * &&
                        git clone -b jenkins https://github.com/Ppablo/ExamenDevops.git &&
                        cd ExamenDevops/src &&
                        docker compose up -d
                        "
                    '''
                }
            }
        }
    }

    post {
        success {
            mail to: 'giradomoran@gmail.com',
                 subject: "Pipeline ejecucion correcta",
                 body: """
                 Hola,

                 El pipeline '${env.JOB_NAME}' (Build #${env.BUILD_NUMBER}) se ejecuto correctamente
                 revisar el siguiente enlace: ${env.BUILD_URL}
                 """
        }
    }
}