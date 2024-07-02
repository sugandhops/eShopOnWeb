pipeline {
    agent any

    tools {
        // Install the .NET SDK
        dotnet 'dotnet-sdk'
    }

    stages {
        stage('Clone') {
            steps {
                // Clone the repository
                git url: 'https://github.com/sugandhops/eShopOnWeb.git'
            }
        }

        stage('Restore') {
            steps {
                // Restore .NET dependencies
                sh 'dotnet restore eShopOnWeb.sln'
            }
        }

        stage('Build') {
            steps {
                // Build the .NET solution
                sh 'dotnet build eShopOnWeb.sln --configuration Release'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh 'dotnet test eShopOnWeb.sln --configuration Release --no-build'
            }
        }

        stage('Publish') {
            steps {
                // Publish the artifacts
                sh 'dotnet publish eShopOnWeb.sln --configuration Release --output ./publish'
                archiveArtifacts artifacts: 'publish/**/*', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            // Notify success
            echo 'Build completed successfully.'
        }
        failure {
            // Notify failure
            echo 'Build failed.'
        }
    }
}
