node {
  withEnv(["HOME=${workspace}"]) {
      stage('Initialize'){
        def dockerHome = tool 'node'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
      }
      // withEnv(['PATH+NODE=C:/Program Files/nodejs/node_modules/npm/bin']) {
      //         stage('Prepare') {
      //         sh "npm install -g yarn"
      //         sh "yarn install"
      //     }
      // } 
      stage("Prepare") {
        checkout scm
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