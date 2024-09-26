pipeline {
    agent any

    stages {
        stage('Clonage du dépôt GitHub') {
            steps {
                git branch: 'main', url: 'https://github.com/GetLoloed/OSDetector.git'
            }
        }

        stage('Installation de Python 3.11 et pip') {
            steps {
                sh '''
                    sudo apt-get update
                    sudo apt-get install -y python3.11 python3-pip
                '''
            }
        }

        stage('Exécution du script Python') {
            steps {
                sh 'python3 os_detector.py'
            }
        }
    }

    post {
        success {
            echo 'It worked, you Geniuuuus !'
        }
        failure {
            echo 'Ohh god, we are in troubles'
            script {
                def emailBody = "Bonjour,\n\nLa construction et l'exécution du script ont échoué. Veuillez vérifier les journaux de construction Jenkins pour plus de détails.\n\nCordialement,\nL'équipe DevOps"
                emailext (
                    subject: 'Échec de la construction Jenkins',
                    body: emailBody,
                    recipientProviders: [[$class: 'CulpritsRecipientProvider']],
                    to: 'loic.aviez91@gmail.com'
                )
            }
        }
    }
}
