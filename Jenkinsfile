pipeline {
  agent  label:'has-docker'

  stages {
    stage("Build") {
      steps {
      echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
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
