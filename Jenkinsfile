node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan atau "Abort" untuk menghentikan)'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            echo 'Aplikasi berjalan selama 1 menit...'
            sleep(time: 1, unit: 'MINUTES')
            echo 'Mengakhiri aplikasi.'
            sh './jenkins/scripts/kill.sh'
        }
    }
}