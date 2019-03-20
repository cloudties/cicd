node {
 	// Clean workspace before doing anything
    deleteDir()
properties([
//pipelineTriggers([pollSCM('H * * * *')])

pipelineTriggers([
        [$class: "SCMTrigger", scmpoll_spec: "H/5 * * * *"],
    ])

])



    try {
        stage ('Clone') {
              echo "added Pooling"
        	checkout scm
        }
        stage ('Build') {
        	bat "echo 'shell scripts to build project...'"
        }
        stage ('Tests') {
	        parallel 'static': {
	            bat "echo 'shell scripts to run static tests...'"
	        },
	        'unit': {
	            bat "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            bat "echo 'shell scripts to run integration tests...'"
	        }
        }
      	stage ('Deploy') {
            bat "echo 'shell scripts to deploy to server...'"
      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}




