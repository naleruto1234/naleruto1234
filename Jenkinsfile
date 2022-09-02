def githubRepo = 'https://github.com/naleruto1234/naleruto1234.git'
def githubBranch = 'master'

def dockerRepo = 'naleruto/webserver-ada'
def dockerHome = tool 'myDocker'

pipeline
{
    agent any
    environment
    {
        dockerImage = ''
    }
    stages
    {
        stage('Git Clone')
        {
            steps
            {
                echo 'Git Clone'
                git url: githubRepo,
                    branch: githubBranch
            }
        }

        stage('Initialize'){
          env.PATH = "${dockerHome}/bin:${env.PATH}"
        }

        stage('Build')
        {
            steps
            {
                echo 'Building...'
                script
                {
                    dockerImage = docker.build("naleruto/webserver-ada:${env.BUILD_ID}", ".")
                }
            }
        }

    }
}
