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
                sh 'apt-get update -qq \
                    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common'
                sh 'curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -'
                sh 'add-apt-repository \
                    "deb [arch=amd64] https://download.docker.com/linux/debian \
                    $(lsb_release -cs) \
                    stable"'
                sh 'apt-get update  -qq \
                    && apt-get install docker-ce'
                sh 'usermod -aG docker jenkins'
                // sh 'sudo apt-get update'
                // sh 'sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin'
                // sh 'apt-cache madison docker-ce'
                // sh 'sudo apt-get install docker-ce=5:20.10.16~3-0~ubuntu-jammy docker-ce-cli=5:20.10.16~3-0~ubuntu-jammy containerd.io docker-compose-plugin'
                // sh 'sudo docker run hello-world'
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