pipeline
{
    agent any
    stages
    {
        stage('continuous download')
        {
            steps
              {
                  script
                  {
                      try
                      {
                        git 'https://github.com/intelliqittrainings/maven.git'  
                      }
                      catch(Exception e1)
                      {
                        System.out.println(e1.getmessage())
                        mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'download step failed', to: 'manasa2116@gmail.com' 
                        exit(1)
                      }
                  }
                
              }
        }      
        
        stage('continuous build')
        {
            steps
              {
                sh 'mvn package'
              }
        }   
        
        stage('continuous deployment')
        {
            steps
            {
             sh 'scp /home/ubuntu/.jenkins/workspace/declarativepipeline/webapp/target/webapp.war ubuntu@172.31.45.145:/var/lib/tomcat9/webapps/testfinal.war'   
            }
        }
        
        stage('continuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/declarativepipeline/testing.jar'
            }
        }
    }
    
        post
        {
            success
            {
                sh 'scp /home/ubuntu/.jenkins/workspace/declarativepipeline/webapp/target/webapp.war ubuntu@172.31.40.37:/var/lib/tomcat9/webapps/prodfinal.war'
            }
            failure
            {
               mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'Jenkins job failed', to: 'manasa6355@gmail.com' 
            }
            
        }
    
}
