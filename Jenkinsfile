/* Jenkinsfile  */

@Library('smartlogic-common@v2') _

smartlogic([
  docker: "maven:3.6.3-jdk-11",
  builder: smartlogic.mavenBuilder(
      args: { getMvnArgs() }
  ),
  parameters: { getParameters() },
  afterBuild: {
      sh "git checkout -f"
  }
])

def getMvnArgs() {
  def args = [
    "-DretryFailedDeploymentCount=10"
  ]
  if (params.QUICKLY) {
    args += "-Dquickly"
  }
  if (params.SKIP_ENFORCER) {
    args += "-Denforcer.skip=true"
  }

  args
}

def getParameters() {
    [
        booleanParam(
          name: 'QUICKLY',
          defaultValue: true
        ),
        booleanParam(
          name: 'SKIP_ENFORCER',
          defaultValue: true
        )
    ]
}