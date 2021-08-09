node ('coreslave') {

    stage('Preparation') {
        timestamps {
            print 'Prepping workspace for build...'
        }

        deleteDir()

        gitBranch = env.BRANCH_NAME ?: 'master'

	    checkout scm
        version = currentBuild.number
        currentBuild.displayName = "#${currentBuild.number}"
    }

    stage('terrafomr Validate') {
        timestamps {
            print 'Running Validation'
        }
        sh "terraform validate"


        timestamps {
            print "terraform Validation CompleteD"
        }
    }

    stage('terraform code scan') {
        
        timestamps {
            print 'terraform code scan'
        }

        sh 'tfsec run'
        
        timestamps {
            print 'terraform scan completed'
        }
    }

    stage('terraform plan'){
        timestamps{
            print "Starting Quality Gate Check"
        }

         sh 'terraform plan'

        }

        timestamps{
            print "terraform plan completed"
        }
    }
}
