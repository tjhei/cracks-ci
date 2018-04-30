pipeline {
  agent  { 
    docker {
      image 'dealii/dealii:v8.5.1-gcc-mpi-fulldepscandi-debugrelease' /*dealii/base:gcc-mpi'*/
	label 'has-docker'
	args '-v /home/docker/jenkins:/home/dealii/jenkins'
	}
  }

  parameters {
    booleanParam(defaultValue: false, description: 'do we trust this user to run the testsuite?', name: 'TRUST_BUILD')
      }
  

  stages
    {
      
    stage("pre") {
      steps {
	echo "Running build ${env.BUILD_ID} on ${env.NODE_NAME}, env=${env.NODE_ENV}"
	  sh 'printenv'
	  echo '${params.TRUST_BUILD}'
	  echo '${TRUST_BUILD}'
	  }
    }
    
    stage ("check") {
      when {
	expression { return "${params.TRUST_BUILD}" == "false" && ! ["a@b.com", "heister@clemson.edu"].contains("${env.CHANGE_AUTHOR_EMAIL}")
	    }
      }
      steps
	{ 
	  echo "please ask an admin to rerun on jenkins with TRUST_BUILD=true"
	    sh "exit 1"
	}
    }

    stage("conf") {
      steps {
	echo "Running build ${env.BUILD_ID} on ${env.NODE_NAME}, env=${env.NODE_ENV}"
	  sh 'printenv'
	  sh 'ls -al'
	  sh 'cmake .'
	  }
    }
    stage("build") {
      steps {
      	sh 'make -j 4'                
	  }
    }
    stage('Test') {
      steps {
	echo 'Testing..'
	  }
    }
  }

  /*
    post
    {
    always
    {
    deleteDir()
    }
    }
  */

}
