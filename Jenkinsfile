pipeline 
{
    agent any 
    
    stages 
    {
        stage('Checkout') 
        {
            steps 
            {
            scm checkout( 'https://github.com/Fleep-6/coursework_2.git')
            }
        }
        stage('Sonarqube') 
        {
    environment 
    {
        scannerHome = tool 'SonarQubeScanner'
    }
    steps {
        withSonarQubeEnv('SonarQube') 
        {
            sh "${scannerHome}/bin/sonar-scanner -D sonar.login=admin -D sonar.password=admin"
        }
        timeout(time: 10, unit: 'MINUTES') 
        {
            waitForQualityGate abortPipeline: true
        }
          }
}
    }
}
