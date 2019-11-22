pipeline {
    agent {
        docker { image 'centos' }
    }
    stages {
        stage('Test') {
            steps {
		sh '''
                cat /etc/*release*
		whoami
		hostname -i
		'''
            }
        }
    }
}
