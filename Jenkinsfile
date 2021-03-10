node {
  withEnv(["HOME=${workspace}"]) {
      stage('Initialize'){
        def dockerHome = tool 'node'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
      }
      stage("Prepare") {
        nodejs('node'){
          checkout scm
          sh 'yarn install'
        }
      }

       stage("Lint") {
         nodejs('node'){
           sh 'yarn nx run-many --target=lint --all'
         }
        
      }

      stage("Test") {
         nodejs('node'){
           sh 'yarn nx run-many --target=test --all'
        } 
      }

     

      stage("Build") {
         nodejs('node'){
            sh 'yarn nx run-many --target=build --all --prod'
         }
       
      }
  }
}