node {
  withEnv(["HOME=${workspace}"]) {
    
      stage('Initialize'){
        def dockerHome = tool 'node'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
      }
      stage("Prepare") {
        checkout scm
        sh "npm install -g yarn"
        sh 'yarn install'
      }

      stage("Test") {
        sh 'yarn nx run-many --target=test --all'
      }

      stage("Lint") {
        sh 'yarn nx run-many --target=lint --all'
      }

      stage("Build") {
        sh 'yarn nx run-many --target=build --all --prod'
      }
  }
}