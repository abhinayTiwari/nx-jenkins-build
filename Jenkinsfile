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
        nodejs('node'){
          checkout scm
          sh 'yarn install'
        }
      }

      stage("Test") {
         nodejs('node'){
           sh 'yarn nx run affected:test -- --base=master --passWithNoTests'
        } 
      }

      stage("Lint") {
         nodejs('node'){
           sh 'yarn nx run-many --target=lint --all'
         }
        
      }

      stage("Build") {
         nodejs('node'){
            sh 'yarn nx run-many --target=build --all --prod'
         }
       
      }
  }
}