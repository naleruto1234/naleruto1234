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
                    docker.withServer('tcp://147.50.143.134:8376') {
                        sh 'C:\WINDOWS\system32\config\systemprofile\AppData\Local\Jenkins.jenkins\workspace\naleruto1234>docker build -t "naleruto/webserver-ada"'
                    }
                }
            }
        }

        // stage('Deploy Image') {
        //     steps{
        //         script {
        //             docker.withServer('tcp://147.50.143.134:8376') {
        //                 docker.withRegistry( '', registryCredential ) {
        //                     dockerImage.push("$BUILD_NUMBER")
        //                     dockerImage.push('latest')
        //                 }
        //             }
        //         }
        //     }
        // }

    }
}