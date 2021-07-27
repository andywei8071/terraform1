pipeline {
    agent {
      node {
        label "master"
      } 
    }

    stages {
      stage('fetch_latest_code') {
        steps {
          git credentialsId: '79ffeae4-a3a4-4b85-86b3-a1929ae3fe21', url: 'https://github.com/andywei8071/terraform1.git'
        }
      }

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
