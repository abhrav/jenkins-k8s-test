node('jenkins-agent') {
    stage('Run shell') {
        container('jnlp') {
        	sh 'ls'
            // sh 'cd /cache && mkdir repo && cd repo'
            // git(url: 'https://github.com/abhrav/jenkins-k8s-test')
        }
        container('docker') {
            // sh 'while [ ! -d "/cache/repo" ]; do sleep 5; done'
            // sh 'cd /cache/repo'
            // sh buildImage(name: 'jenkins-master')
        }
    }
}
