node {
   def mvnHome
   def dockerHome
   stage('Preparation') {
      checkout scm    
      mvnHome = tool 'M3'
      dockerHome = tool 'dockerlatest'
   }
   
   stage('Build') {
        // Run the maven build
        sh "'${mvnHome}/bin/mvn' -f helloworld-html5/pom.xml -Dmaven.test.failure.ignore clean package"
        // Run the docker build and push the image with a branch tag
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'artifactory', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
            sh "sudo '${dockerHome}/bin/docker' login -u $USERNAME -p $PASSWORD localhost:8081"
        }
        sh "sudo '${dockerHome}/bin/docker' build -t localhost:8081/docker-snapshots:${BRANCH_NAME} -f helloworld-html5/Dockerfile ."
        sh "sudo '${dockerHome}/bin/docker' push localhost:8081/docker-snapshots:${BRANCH_NAME}"
   }
}