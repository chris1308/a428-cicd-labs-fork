node {
    // Docker container setup
    def dockerImage = 'node:16-buster-slim'
    def dockerArgs = '-p 3001:3001'

    try {
        // Using Docker container for the pipeline
        docker.image(dockerImage).inside(dockerArgs) {
            // Ensure we're in the right directory where package.json exists
            dir("${env.WORKSPACE}") {
                stage('Build') {
                    // Ensure npm install is run inside the right directory
                    sh 'npm install'
                }

                stage('Test') {
                    // Run tests from the appropriate directory
                    sh './jenkins/scripts/test.sh'
                }
            }
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}
