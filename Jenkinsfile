pipeline {
  agent  { 
  docker {
  image 'dealii/base:gcc-mpi'
  	 label 'has-docker'
	 args '-v /home/docker/jenkins:/home/dealii/jenkins'
	 }
  }

  stages {
    stage("Build") {
      steps {
      echo "Running build ${env.BUILD_ID} on ${env.JENKINS_URL}, env=${env.NODE_ENV}"
      sh 'printenv'
        sh 'ls -al'
      	sh 'cmake .'
        sh 'ls -al'
      	sh 'make -j 4'
      }
      }
      stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
    }

post
{
    always
    {
      deleteDir()
    }
}
}
