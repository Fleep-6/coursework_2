pipeline 
{
    agent { docker { image 'node:6.3' } }
    stages 
    {
        stage('build') 
        {
            steps 
            {
            sh'npm install'
            sh'node server.js'
            }
        }
        stage('Sonarqube') 
        {
    environment 
    {
        scannerHome = tool 'SonarQubeScanner'
    }
    steps {
        withSonarQubeEnv('sonarqube') 
        {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES') 
        {
            waitForQualityGate abortPipeline: true
        }
          }
}
    }
}
