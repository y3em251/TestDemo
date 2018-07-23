node {
    // Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Code cloning') {
            checkout scm
        }
        stage ('connect to server') {
            sh "echo 'shell scripts to build project...'"
	    sh '''ssh -t santosh@production-box 
	    cd /tmp  
	    touch pipe1 pipe2 '''
        }
        stage (' Build ') {
            parallel 'static': {
                sh "echo 'shell scripts to run static tests...'"
            },
            'unit': {
                sh "echo 'shell 2 scripts to run unit tests...'"
            },
            'integration': {
                sh "echo 'shell scripts to run integration tests...'"
            }
        }
        stage ('Deploy') {
            sh "echo 'shell 1 scripts to deploy to server...'"
        }
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}

