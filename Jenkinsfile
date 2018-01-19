node {
   def mvnHome
   def dockerHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      checkout scm
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
      dockerHome = tool 'dockerlatest'
   }
   
   stage('Build') {
        // Run the maven build
        sh "'${mvnHome}/bin/mvn' -f helloworld-html5/pom.xml -Dmaven.test.failure.ignore clean package"
        sh "sudo '${dockerHome}/bin/docker' build -t localhost:8081/docker-snapshots:${BRANCH_NAME} -f helloworld-html5/Dockerfile ."
        //sh "sudo '${dockerHome}/bin/docker' push localhost:8081/docker-snapshots:latest -f helloworld-html5/Dockerfile ."
        //docker.build("localhost:8081/docker-snapshots:latest", "-f helloworld-html5/Dockerfile .")
   }
}