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


}
