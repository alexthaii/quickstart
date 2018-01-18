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
      dockerHome = tool 'docker'
   }
   stage('Build') {
        // Run the maven build
        sh "'${mvnHome}/bin/mvn' -f helloworld-html5/pom.xml -Dmaven.test.failure.ignore clean package"
        // Run docker build
        app = sh "'${dockerHome}/bin/docker' build -t localhost:8081/docker-snapshots/helloworld helloworld-html5/Dockerfile"
   }
}