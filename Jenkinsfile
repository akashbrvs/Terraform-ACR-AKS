pipeline {
     agent any
	 options{
        buildDiscarder(logRotator(numToKeepStr: '7', daysToKeepStr: '7'))
        timestamps()
        }
     
        environment {
		ENV="qa"
    }
    
    stages {

        stage ('1-GITHUB-Repo-checkout') {
            steps {
              git (url:'https://github.com/akashbrvs/Terraform-ACR-AKS.git', branch: 'main', credentialsId: 'GITHUB')
            }
        }
		stage ('2-Terraform-Provision') {
		when{
		      expression {ACTION == 'provision '}
		    }
            steps {
              sh 'sh terraform.sh'
            }
        }
		
		stage ('2-Terraform-de-provision') {
		when{
		      expression {ACTION == 'de-provision  '}
		    }
            steps {
              sh 'terraform destroy -auto-approve'
			  sh '''
			      rm terraform.tfstate
                  rm terraform.tfstate.backup
                  rm .terraform.lock.hcl
                  rm tfplan
                  rm tfplan.json
                  rm -r .terraform/
				  '''
            }
        }
      
    }
  
 }
