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
    		sh 'pip install s3cmd'
    		sh 's3cmd get s3://dataxu-artifacts/jenkins/secure_dev.tar.gz.gpg'
			sh 'gpg --batch --yes --passphrase dataxu -o secure_dev.tar.gz secure_dev.tar.gz.gpg'
			sh 'tar xzf secure_dev.tar.gz'
			sh 'ls secure_dev/'
			sh 'cat secure_dev/config'
			sh 'cat secure_dev/awscreds'
			sh 'mkdir ~/.aws'
			sh 'mv secure_dev/config ~/.aws/config'
			sh 'export KOPS_STATE_STORE=s3://k8s-jenkins-useast1_devaws_dataxu_net&&kops export kubecfg k8s-jenkins-useast1.devaws.dataxu.net'
			sh 'kubectl config view'
			sh 'kubectl cluster-info'
		}
	}
}

