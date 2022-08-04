pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'k8s', url: 'https://github.com/Niroth36/django3-sampe-project.git'

                
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
            environment {
                IMAGE='tsadimas/django'
            }
            steps {
                sh '''
                echo $BUILD_ID
                COMMIT_ID=$(git rev-parse --short HEAD)
                echo $COMMIT_ID
                TAG=$COMMIT_ID-$BUILD_ID
                docker build -t $IMAGE -t $IMAGE:$TAG .
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
