def imageName = "quay.io/halkeye/gavinmogan-dot-com";
properties([[$class: 'GithubProjectProperty', displayName: '', projectUrlStr: 'https://github.com/halkeye/gavinmogan.com/']])

node {
  def commitHash
  def branchName
  stage('Checkout') {
    /* Checkout the code we are currently running against */
    def scmVars = checkout(scm)
    commitHash = scmVars.GIT_COMMIT.take(6)
    branchName = scmVars.GIT_BRANCH
  }

  stage('Build') {
    /* Build the Docker image with a Dockerfile, tagging it with the build number */
    sh "bower install"
    sh "npm run test"
    sh "npm run build"
  }
}
