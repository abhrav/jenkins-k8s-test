node('jenkins-agent') {
    stage('Get source') {
        container('jnlp') {
            sh 'cd /cache && mkdir repo && cd repo'
            git(url: 'https://github.com/abhrav/jenkins-k8s-test')
        }
    }
    stage('Build and push image') {
    	container('docker') {
            sh 'cd /cache/repo'
            sh 'docker build -t abhrav/jenkins-master .'
            sh 'docker login -u abhrav -p qwerty11'
            sh 'docker push abhrav/jenkins-master'
        }
    }
    stage('Deploy new master to k8s') {
    	container('k8s-accessor') {
    		sh 'kubectl cluster-info'
    		sh 'kubectl proxy &'
    		sh 'kubectl cluster-info'
		}
	}
}

