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
                echo 'Instal Docker..'
                sh 'cat /etc/os-release'
                sh 'curl -fsSL "https://download.docker.com/linux/static/stable/x86_64/docker-17.03.1-ce.tgz" \
                    | tar -xzC /usr/local/bin --strip=1 docker/docker'
                sh 'sudo service docker start'
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