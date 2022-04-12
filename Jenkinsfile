def artifactory_name = "artifactory"
def artifactory_repo = "conantest"
def repo_url = 'https://github.com/codeQueries/training.git'
def repo_branch = "master"
def recipe_folder = "create"
def consume_folder = "consumer"
def channel = "hello/0.1"
def user = "user/testing"


node('jenkins-slave') {
    
    // Clone the code from github:
        git url :'https://github.com/codeQueries/training.git'

        // Obtain an Artifactory server instance, defined in Jenkins --> Manage Jenkins --> Configure System:
        def server = Artifactory.server artifactory_name

        // Create a local build-info instance:
        def buildInfo = Artifactory.newBuildInfo()
        buildInfo.name = "Conan-pipeline"

        // Create a conan client instance:
        def conanClient = Artifactory.newConanClient()

        // Add a new repository named 'conan-local' to the conan client.
        // The 'remote.add' method returns a 'serverName' string, which is used later in the script:
        String serverName = conanClient.remote.add server: server, repo: "conantest"

        // Run a conan build. The 'buildInfo' instance is passed as an argument to the 'run' method:
        dir (consume_folder) {
            conanClient.run(command: "install . --build missing", buildInfo: buildInfo)

        // Create an upload command. The 'serverName' string is used as a conan 'remote', so that
        // the artifacts are uploaded into it:
            String command = "upload * --all -r ${serverName} --confirm"

        // Run the upload command, with the same build-info instance as an argument:
            conanClient.run(command: command, buildInfo: buildInfo)

         // Publish the build-info to Artifactory:
            server.publishBuildInfo buildInfo
        }
}
