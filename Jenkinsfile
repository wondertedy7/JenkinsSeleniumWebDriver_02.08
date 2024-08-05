pipeline {
    agent any

    stages{
        stage("Checout code") {
            //checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/wondertedy7/JenkinsSeleniumWebDriver_02.08'
            }
        }
        stage("Setup .Net Core") {
            //install dotnet
            steps {
                bat '''
                echo Downloading .NET SDK 6.0
                curl -l -o dotnet-sdk-6.0.424-win-x86.exe https://download.visualstudio.microsoft.com/download/pr/9e184641-56bb-430b-9297-4316b039b641/3409ae071e0140ce2237f909b4b0ffbb/dotnet-sdk-6.0.424-win-x86.exe
                echo Installing .NET SDK 6.0
                dotnet-sdk-6.0.424-win-x86.exe /quiet /norestart
                '''   
            }

        }
        stage("Restore nuget packages") {
            steps {
                bat 'dotnet restore SeleniumBasicExercise.sln'
            }

        }
        stage("Build") {
            //build
            steps {
                bat 'dotnet build SeleniumBasicExercise.sln --configuration release'
            }
        }
        stage("Run Tests TestProject1") {
            //run tests
            steps {
                bat 'dotnet test TestProject1/TestProject1.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
        stage("Run Tests TestProject2") {
            //run tests
            steps {
                bat 'dotnet test TestProject2/TestProject2.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
        stage("Run Tests TestProject3") {
            //run tests
            steps {
                bat 'dotnet test TestProject3/TestProject3.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            junit '**/TestResults/*.trx'
        }
    }
}