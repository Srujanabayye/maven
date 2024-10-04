pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: '6f71fcaf-83aa-4099-9784-6a65c7c8e637', path: '', url: 'http://172.31.17.222:8080')], contextPath: 'mytest', war: '**/*.war'
	    }
        }
        stage('ContinuousTesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
       
    }
    
    post
    {
        success
        {
            deploy adapters: [tomcat9(credentialsId: '6f71fcaf-83aa-4099-9784-6a65c7c8e637', path: '', url: 'http://172.31.18.23:8080')], contextPath: 'myprod', war: '**/*.war'

        }
        failure
        {
            mail bcc: '', body: 'Continuous Integration has failed', cc: '', from: '', replyTo: '', subject: 'CI Failed', to: 'nicybayye19@gmail.com'
        }
       
    }
    
    
    
    
    
    
}
