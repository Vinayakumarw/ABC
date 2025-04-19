pipeline {
    agent any

    environment {
        MAVEN_REPO = 'https://pkgs.dev.azure.com/vinayavrikodhara2366/demo-project/_packaging/vinayakumar/maven/v1'
        TOMCAT_WEBAPPS_DIR = '/home/vinay/tomcat/apache-tomcat-9.0.98/webapps'
        GIT_URL = 'https://github.com/Vinayakumarw/ABC.git'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: "${GIT_URL}"
            }
        }

        stage('Build Project') {
            steps {
                script {
                    sh 'mvn clean install'
                }
            }
        }

        stage('Push Artifact to Repository') {
            steps {
                script {
                    sh """mvn deploy:deploy-file -X -s settings-temp.xml -Dfile=/home/vinay/ABC/ABC-1611/target/ABC-1611-1.0.0.jar -DgroupId=com.example -DartifactId=ABC-1611 -Dversion=1.0.4 -Dpackaging=jar -DrepositoryId=vinayakumar -Durl=https://pkgs.dev.azure.com/vinayavrikodhara2366/demo-project/_packaging/vinayakumar/maven/v1"""

                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Copy .war file to Tomcat's webapps directory
                    sh "sudo cp /home/vinay/ABC/ABC-1611/target/ABC-1611-1.0.0.jar ${TOMCAT_WEBAPPS_DIR}"

                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed successfully!'
        }
    }
}
