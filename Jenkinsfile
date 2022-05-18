pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/JoyOrji1/newjava.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins is unable to download the development code from remote github', cc: '', from: '', replyTo: '', subject: 'Download failed', to: 'git.admin@gmail.com'
                        exit(1)
                    }
                }
                
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artifact from the code', cc: '', from: '', replyTo: '', subject: 'Build failed', to: 'dev.team@gmail.com'
                        exit(1)
                    }
                }
                
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '03c901c1-2399-4427-ad28-9e402b5dbea0', path: '', url: 'http://172.31.29.11:8080')], contextPath: 'test2', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on QA server', cc: '', from: '', replyTo: '', subject: 'Deployment failed', to: 'middleware.team@gmail.com'
                    }
                }
                
            }
        }
        stage('Continuoustesting')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                        sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selenium test script are giving a failure status', cc: '', from: '', replyTo: '', subject: 'Testing failed', to: 'qa.team@gmail.com'
                        exit(1)
                    }
                }
                
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '03c901c1-2399-4427-ad28-9e402b5dbea0', path: '', url: 'http://172.31.19.88:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on prodserver', cc: '', from: '', replyTo: '', subject: 'Delivery failed', to: 'delivery.team@gmail.com'
                    }
                }
                
            }
        }
    }
}
