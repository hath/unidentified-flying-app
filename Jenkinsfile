node {
	try {
		notifyBuild('STARTED')

		setBuildStatus("In progress...", "PENDING");

		stage('Checkout') {
			checkout scm
		}

		stage('Client tests') {
			sh "npm test"
		}

	} catch (e) {
		setBuildStatus(e.take(140), "FAILURE");
		currentBuild.result = "FAILED"
		throw e
	} finally {
  		setBuildStatus("Success", "SUCCESS");
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
    }

    // Send notifications
    slackSend (color: colorCode, message: subject)

}
