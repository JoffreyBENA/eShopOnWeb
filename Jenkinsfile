pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'dotnet test eShopOnWeb.sln '
      }
    }

    stage('Tests') {
      parallel {
        stage('Unit') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/integrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish eShoponWeb.sln -o /var/aspnet'
      }
    }

  }
}