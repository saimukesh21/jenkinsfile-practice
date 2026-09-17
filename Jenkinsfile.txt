pipeline {

    agent any

    stages {

        stage('Start') {
            steps {
                echo 'Jenkinsfile Pipeline Started'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'

                bat '''
                    echo Creating build file...
                    echo Jenkinsfile Build > build.txt
                    echo Build completed successfully.
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'

                bat '''
                    echo Checking build file...

                    if exist build.txt (
                        echo Build file found.
                        echo Test passed successfully.
                    ) else (
                        echo Build file not found.
                        exit /b 1
                    )
                '''
            }
        }

        stage('Finish') {
            steps {
                echo 'Jenkinsfile Pipeline completed successfully!'
            }
        }

    }
}