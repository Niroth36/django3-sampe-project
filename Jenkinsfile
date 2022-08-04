pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/Niroth36/django3-sampe-project.git'

                
            }
        }
        
        stage('Test') {
            steps {
                sh '''
                    python3 -m venv myvenv
                    source myvenv/bin/activate
                    pip install -r requirements.txt
                    cd myproject
                    cp myproject/.env.example myproject/.env
                    ./manage.py test'''
            }
        }

        // stage ('Deploy') {
        //     steps {
        //         sshagent (credentials: ['ssh-deployment-1']) {

        //         sh '''
        //             pwd
        //             ansible-playbook -i ~/workspace/ansible-project/hosts.yml -l deploymentservers ~/workspace/ansible-project/playbooks/control.yml
        //             '''
        //     }
        //     }
        // }
        stage ('Docker create and push image') {
            steps {
                sh '''
                docker build -t tsadimas/django .
                '''
            }
        }

        stage ('Deploy to k8s') {
            steps {
                sh '''
                kubectl get pods
                '''
            }
        }
    }
}
