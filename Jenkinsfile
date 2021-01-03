pipeline {
  agent {
    docker {
      image 'hashicorp/terraform:light'
      args '--entrypoint='
    }
  }

  stages {
    stage('Terraform Plan') { 
      steps {
           withAWS(credentials:'terraform'){
             
            sh 'printenv'
            sh 'cd tf_code && terraform plan -no-color -out=create.tfplan'
         
        }
      }
    }
    // Optional wait for approval
    //input 'Deploy stack?'

    stage ('Terraform Apply') {
      steps{
        withAWS(credentials:'terraform'){
            sh "terraform apply -input=false tfplan"
        }
      }
    }
  }
}
