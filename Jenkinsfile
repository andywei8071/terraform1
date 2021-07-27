pipeline {
    agent {
      node {
        label "master"
      } 
    }

    stages {
      stage('TF Init&Plan') {
        steps {
          sh '/usr/local/bin/terraform init'
          sh '/usr/local/bin/terraformterraform plan'
        }      
      }

      stage('Approval') {
        steps {
          script {
            def userInput = input(id: 'confirm', message: 'Apply Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
          }
        }
      }

      stage('TF Apply') {
        steps {
          sh 'terraform apply -input=false'
        }
      }
    } 
  }
