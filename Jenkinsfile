pipeline{
  agent any
  environment{
    PYTHON_PATH = 'C:\\Program Files\\Python313;C:\\Program Files\\Python313\\Scripts'
  }
  stages{
    stage('Checkout'){
      steps{
        checkout scm
      }
    }
    stage('Build'){
      steps{
        bat '''
        set PATH = %PYTHON_PATH%;%PATH%
        pip install -r requirements.txt
        '''
      }
    }
    stage('SonarAnalysis'){
      environment{
        SONAR_TOKEN = credentials('sonar-token')
      }
      steps{
        bat '''
        set PATH = %PYTHON_PATH%;%PATH%
        sonar-scanner -Dsonar.projectKey=Pipeline
        -Dsonar.sources=.
        -Dsonar.host.url=http://localhost:9000
        -Dsonar.token=sqp_3c6e711ba6a5ce91b446286acdb59844185b19d0"
        '''
      }
    }
  }
  post{
    success{
      echo "Successfully executed"
    }
    failure {
      echo "Did not work"
    }
  }
}
