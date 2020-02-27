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
               sh label: '', script: 'scp /var/lib/jenkins/workspace/multipipeline_master@2/target/hello-1.16.war /opt/tomcat/tomcat/webapps jenkins@172.31.81.192'
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
              sh label: '', script: 'scp /var/lib/jenkins/workspace/multipipeline_master@2/target/hello-1.16.war jenkins@172.31.94.14:/root'
            }
        }
    }
}
