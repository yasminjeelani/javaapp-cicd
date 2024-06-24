pipeline {
    agent any
 
    stages {

        stage ('Docker login & Building image') {
            steps {
                sh ' docker login -u $DOCKER_USER -p $DOCKER_PASS '
                sh 'docker build -t yasminjeelani/myjavaimage:v1 .'
            }
        }

        stage ('Pushing the Docker image to DockerHub') {
            steps {
                sh 'docker push yasminjeelani/myjavaimage:v1'
            }
        }
        
        stage('Deploy to Deployment server') {
            steps {
                script {
                    sshagent(['ssh']) {
                        // Execute the command within the sshagent block using sh step
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.233.238.185 "docker run -d -it --name javaapp -p 80:8080 yasminjeelani/myjavaimage:v1"'
                    }
                }
            }
        }
    }
}
