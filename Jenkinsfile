pipeline {
    agent any
    stages {
        // [START tf-init, tf-validate]
        stage('TF init & validate') {
            when { anyOf {branch "prod";branch "dev";changeRequest() } }
            steps {
                sh '''
                terraform init
                terraform validate
                '''
            }
        }
        // [END tf-init, tf-validate]

        // [START tf-plan]
        stage('TF plan') {
            when { anyOf {branch "prod";branch "dev";changeRequest() } }
            steps {
                sh '''
                terraform plan
                '''
            }
        }
        // [END tf-plan]

        stage('Terratest') {
            when { anyOf {branch "prod";branch "dev";changeRequest() } }
            steps {
                sh '''
                echo "your test caces cann run here"
                '''
            }
        }

        
        // [START tf-apply, tf-destroy]
        stage('TF Apply') {
            when { anyOf {branch "prod";branch "dev" } }
            steps {
                sh '''
                terraform apply -auto-approve
                terraform destroy -auto-approve
                '''
            }
        }
        // [END tf-apply, tf-destroy]
  }
}
