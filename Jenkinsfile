pipeline {
    agent any
    stages {
	    
        stage('Lint HTML') {
            steps {
                sh 'tidy -q -e *.html'
            }
		}
        
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    sh 'docker build . -t homac/udacity-cloud-devops-capstone'
                    }
                }
        }
             
        stage('Push Docker Image') {
             when {
                branch 'master'
            }
            steps {
                script {
                    withDockerRegistry( credentialsId: "docker_hub_login") {
                        sh 'docker tag homac/udacity-cloud-devops-capstone:latest homac/udacity-capstone-project'
                        sh 'docker push homac/udacity-cloud-devops-capstone'
                    }
                }
            }
        }

        stage('Deploy to k8s') {
            when {
                branch 'master'
            }
            steps {
                script {
                    sh 'curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl'
                    sh 'chmod +x ./kubectl'
                    sh 'sudo mv ./kubectl /usr/local/bin/kubectl'
                    sh 'kubectl --kubeconfig /var/lib/jenkins/.kube/eks-example get pods'
                }
            }
        }	    

    }
}

