def group = "it"
def service = "go"
def namespace = "${group}/${service}"
def imageName
def docImageName
def imageVersion
def docImageVersion
def releaseTag

builderNode {
  stage("Build Image") {
    checkout scm
    imageVersion = lendupVersion()
    imageName = buildLendupDockerImage(
      artifactory: true,
      repository:  "it/go",
      dockerfile: "Dockerfile"
    )
  }
}

builderNode {

  if (env.BRANCH_NAME == "master") {

    stage("Promote") {
      promoteLendupDockerImage(
        artifactory: true,
        imageName: imageName,
        toTags: [imageVersion, "latest"],
        registry: "docker-builds"
      )
    }
}
