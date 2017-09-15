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
	buildStatus = buildStatus ?: 'SUCCESSFUL'

	emailext (
		subject: "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
		body: """<p>${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' </p> Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
		recipients: ${DEFAULT_RECIPIENTS}
	)
}
