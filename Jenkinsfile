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
        stage('initialsie')
        {
            steps
            {
                sh '''
                echo "PATH = ${PATH}"
                echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('Build')
        {
            steps
            {
                sh 'mvn -Dmaven.test.failure.ignore=true install'
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
