node {
   def mvnHome
   def dockerHome
   def dockerTag
   stage('Preparation') {
      checkout scm    
      mvnHome = tool 'M3'
      dockerHome = tool 'dockerlatest'
   }
   
   script {
        def get_tag = $/eval 'echo ${BRANCH_NAME} | sed "s/^release\/\(.\+\)/\1/g; s/[^0-9A-Za-z.]/-/g")'/$
        //dockerTag = sh(script: "${get_tag}", returnStdout: true)
   }

   stage('Build') {
        // Run the maven build
        sh "'${mvnHome}/bin/mvn' -f helloworld-html5/pom.xml -Dmaven.test.failure.ignore clean package"
        // Run the docker build and push the image with a branch tag
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'artifactory', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
            sh "sudo '${dockerHome}/bin/docker' login -u $USERNAME -p $PASSWORD localhost:8081"
        }
        
        sh "sudo '${dockerHome}/bin/docker' build -t localhost:8081/docker-snapshots/helloworld:${dockerTag} -f helloworld-html5/Dockerfile ."
        sh "sudo '${dockerHome}/bin/docker' push localhost:8081/docker-snapshots/helloworld:${dockerTag}"
   }
}