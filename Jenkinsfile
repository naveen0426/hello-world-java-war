pipeline
{
    agent any
    stages
    {
        stage('ContinousDownload')
        {
            steps
            {
               git 'https://github.com/naveen0426/hello-world-java-war.git' 
            }
        }
        stage('ContinousBuild')
        {
            steps
            {
               sh 'mvn -v'
            }
        }
        stage('ContinousDeployment')
        {
            steps
            {
               sh label: '', script: 'scp /var/lib/jenkins/workspace/Multibranch/target/*.war ec2-user@18.205.152.8:/opt/tomcat/tomcat/webapps/*.war'
            }
        }
        stage('ContinousTesting')
        {
            steps
            {
                git 'https://github.com/naveen0426/FunctionalTesting.git'

                sh label: '', script: 'echo "Testing Passed"'
            }
        }
         stage('ContinousDelivery')
        {
            steps
            {
              sh label: '', script: 'scp /var/lib/jenkins/workspace/Multibranch/target/*.war ec2-user@3.92.179.220:/root/*.war'
            }
        }
    }
}
