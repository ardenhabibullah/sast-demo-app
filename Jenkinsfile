pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ardenhabibullah/sast-demo-app.git', branch: 'master'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install bandit'
            }
        }

        stage('SAST Analysis') {
            steps {
                // Menjalankan Bandit dan menghasilkan output XML
                sh '/usr/bin/bandit -f xml -o bandit-output.xml -r .'
                
                // Menggunakan recordIssues untuk melaporkan hasil analisis
                recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
            }
        }
    }
}
