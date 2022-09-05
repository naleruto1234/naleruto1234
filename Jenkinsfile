def githubRepo = 'https://github.com/naleruto1234/naleruto1234.git'
def githubBranch = 'master'

def dockerRepo = 'naleruto/webserver-ada'

pipeline
{
    agent any
    environment
    {
        imagename = "naleruto/webserver-ada"
        registryCredential = 'naleruto-dockerhub'
        dockerImage = ''
    }
    stages
    {

        stage('Instal Docker')
        {
            steps
            {
                agent {
                        docker { image 'docker:latest' }
                }
                steps {
                    echo 'Instal Docker..'
                    sh 'docker run --rm --network some-network \
                            -e DOCKER_TLS_CERTDIR=/certs \
                            -v some-docker-certs-client:/certs/client:ro \
                            docker:latest version'
                }
            }
        }


        stage('Git Clone')
        {
            steps
            {
                echo 'Git Clone'
                git url: githubRepo,
                    branch: githubBranch
            }
        }

        stage('Build')
        {
            steps
            {
                echo 'Building...'
                script
                {
                    dockerImage = docker.build imagename
                }
            }
        }

        stage('Deploy Image') {
            steps{
                script {
                docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("$BUILD_NUMBER")
                    dockerImage.push('latest')

                }
                }
            }
        }

    }
}