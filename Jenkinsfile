node {
    properties([disableConcurrentBuilds()])
    try {
        stage('Initialize') {
            sh 'composer --version'
            sh 'php --version'
            checkout scm
        }
        stage('Install') {
            sshagent(['git_bitbucket.strg.at']) {
                sh 'composer install --ignore-platform-reqs --no-progress --no-scripts'
            }
        }
        stage('Build') {
            sshagent(['git_bitbucket.strg.at']) {
                sh 'composer build'
            }
        }
        stage('Deploying') {
            sshagent(["satis_rsync"]) {
                for (String host : config.HOSTS) {
                    sh "rsync -a --delete --exclude=.git* --delete-excluded output/* satis@srv-registry.strg.at:/home/satis/"
                }
            }
        }
    } catch (all) {
        currentBuild.result = 'FAILURE'
        echo "deploy failed: ${all}"
    }
    stage('Cleanup') {
        cleanWs()
    }
}
