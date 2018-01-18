node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      checkout scm
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'ls'"
         sh "'pwd'"
         sh "'${mvnHome}/bin/mvn -f ${workspace}/helloworld-html5/pom.xml' -Dmaven.test.failure.ignore clean package"
      }
   }
}