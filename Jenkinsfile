node('jenkins-agent') {
    stage('Run shell') {
        container('jnlp') {
        	sh 'cd /cache && mkdir repo && cd repo'
            git(url: 'https://github.com/abhrav/jenkins-k8s-test')
            sh 'mkdir /cache/done'
        }
        container('docker') {
            sh 'while [ ! -d "/cache/done" ]; do sleep 5; done'
            sh 'cd /cache/repo'
            sh 'docker build -t jenkins-master-1 .'
            sh 'docker push abhrav/jenkins-master-1'
        }
    }
}
