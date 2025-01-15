node {
    // Docker container setup
    def dockerImage = 'node:16-buster-slim'
    def dockerArgs = '-p 3001:3001'

    try {
        // Using Docker container for the pipeline
        docker.image(dockerImage).inside(dockerArgs) {
            stage('Build') {
                // Install dependencies
                sh 'npm install'
            }

            stage('Test') {
                // Run tests
                sh './jenkins/scripts/test.sh'
            }
        }
    } catch (Exception e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}
