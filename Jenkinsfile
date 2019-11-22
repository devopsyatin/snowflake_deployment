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
		echo "ls before copy"; ls; pwd
		cp $WORKSPACE/* /opt/SP/apps/.
		ls /opt/SP/apps
		'''
            }
        }
    }
}
