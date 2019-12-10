pipeline 
{
    agent any 
    
    stages 
    {
        stage('Checkout') 
        {
            steps 
            {
           checkout([$class: 'GitSCM',
                     branches: [[name: '*/master']],
                     doGenerateSubmoduleConfigurations: false,
                     extensions: [],
                     submoduleCfg: [],
                     userRemoteConfigs: [[url: 'https://github.com/Fleep-6/coursework_2.git']]])
            }
        }
        stage('Sonarqube Testing') 
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
        
        stage('Docker Build and Push')
        {
            steps
          {
              script
              {
            def app = docker.build("fleep6/coursework2")
            docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_credentials') 
            {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            }
              }
          }
        }
    }
}
