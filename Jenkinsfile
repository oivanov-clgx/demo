node {
   def mvnHome
  stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/ivanov-aleksander/demo.git'
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
              "target": "demo/${BUILD_ID}/"
            }
         ]
        }"""
      server.upload(uploadSpec)
   }


  }
