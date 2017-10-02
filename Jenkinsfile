node {
	try {
		notifyBuild('STARTED')

		stage('Checkout') {
			checkout scm
		}

		stage('Client tests') {
			sh "npm test"
		}

	} catch (e) {
		currentBuild.result = "FAILED"
		throw e
	} finally {
		notifyBuild(currentBuild.result)
	}

}

def notifyBuild(String buildStatus = 'STARTED') {
    // build status of null means successful
    buildStatus =  buildStatus ?: 'SUCCESSFUL'

    // Default values
    def colorName = 'RED'
    def colorCode = '#FF0000'
    def subject = "${buildStatus}: Job '${env.JOB_NAME} Build: ${env.BUILD_NUMBER}'"

    // Override default values based on build status
    if (buildStatus == 'STARTED') {
        color = 'YELLOW'
        colorCode = '#FFFF00'
    } else if (buildStatus == 'SUCCESSFUL') {
        color = 'GREEN'
        colorCode = '#00FF00'
    } else {
        color = 'RED'
        colorCode = '#FF0000'
    }

    // Send notifications
    slackSend (color: colorCode, message: subject)

}
