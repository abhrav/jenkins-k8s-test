node('jenkins-agent') {
    stage('Run shell') {
        container('jnlp') {
        	sh 'cd /cache && mkdir repo && cd repo'
            git(url: 'https://github.com/abhrav/jenkins-k8s-test')
        }
        container('docker') {
            sh 'cd /cache/repo'
            sh 'docker build -t jenkins-master-1 .'
            sh 'docker login -u abhrav -p qwerty11'
            sh 'docker push abhrav/jenkins-master-1'
        }
    }
}
