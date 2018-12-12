node {
    def mvnHome
    stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git url: 'git@github.com:ivanov-aleksander/demo.git', credentialsId: '4f370640-2df2-4fad-8a01-d018d1bdfb6d'
      mvnHome = tool 'M3'
  }

    stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
  }
  
    stage('Upload') {
        def server = Artifactory.server 'artifacotry.vm'
        def uploadSpec = """{
          "files": [
            {
              "pattern": "target/*.jar",
              "target": "demo/app_${BUILD_ID}.jar"
            }
         ]
        }"""
      server.upload(uploadSpec)
   }


  }
//
