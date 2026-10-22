pipeline {
    agent any

    parameters {
        booleanParam(
            name: 'RUN_EXTRA_CHECK',
            defaultValue: true,
            description: 'Run the extra dashboard check'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Thamaraiselvan-26/A.git'
            }
        }

        stage('Build and Test') {
            parallel {
                stage('Check HTML') {
                    steps {
                        sh 'test -s index.html'
                        sh 'grep -q "Smart Campus Energy Monitoring" index.html'
                        echo 'HTML check passed'
                    }
                }

                stage('Check Dockerfile') {
                    steps {
                        sh 'test -s Dockerfile'
                        sh 'grep -q "nginx" Dockerfile'
                        echo 'Dockerfile check passed'
                    }
                }
            }
        }

        stage('Extra Check') {
            when {
                expression { params.RUN_EXTRA_CHECK }
            }
            steps {
                sh 'grep -q "Academic Block" index.html'
                echo 'Extra dashboard check passed'
            }
        }
    }
}
