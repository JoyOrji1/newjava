@Library('library') _

pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload_Loans')
        {
            steps
            {
                script
                {
                    cicd.newGit("https://github.com/JoyOrji1/newjava.git")
                }
            }
        }
        stage('ContinuousBuild_Loans')
        {
            steps
            {
                script
                {
                    cicd.newMaven()
                }
            }
        }
        
    }
}
