pipeline {
    agent any
    
    environment {
        DOTNET_VERSION = '6.0.x'
    }
    
    stages {
       
        stage('Setup .NET') {
            steps {
                script {
                    sh 'wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh'
                    sh 'chmod +x dotnet-install.sh'
                    sh './dotnet-install.sh --version ${DOTNET_VERSION}'
                    sh 'export PATH="$HOME/.dotnet:$PATH"'
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
        
        stage('Run tests') {
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
