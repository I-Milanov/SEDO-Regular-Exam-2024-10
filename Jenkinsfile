pipeline {
    agent {
        label 'ubuntu-latest'
    }
    
    environment {
        DOTNET_VERSION = '6.0.x'
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        
        stage('Setup .NET') {
            steps {
                script {
                    sh 'wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh'
                    sh 'chmod +x dotnet-install.sh'
                    sh './dotnet-install.sh --channel $DOTNET_VERSION'
                    sh 'export PATH=$HOME/.dotnet:$PATH'
                }
            }
        }
        
        stage('Restore dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }
        
        stage('Build') {
            steps {
                sh 'dotnet build --no-restore'
            }
        }
        
        stage('Run Unit Tests') {
            steps {
                sh 'dotnet test HouseRentingSystem.UnitTests/HouseRentingSystem.UnitTests.csproj --no-build --verbosity normal'
            }
        }
    }
}
