pipeline {
    agent {
        node {
            label 'built-in'
            customWorkspace '/mnt/project'
        }
    }

    environment {
        MAVEN_HOME = '/mnt/build-tool/apache-maven-3.9.7'
        M2_HOME = '/mnt/build-tool/apache-maven-3.9.7'
        M2 = '/mnt/build-tool/apache-maven-3.9.7/bin'
        PATH = "/mnt/build-tool/apache-maven-3.9.7/bin:$PATH"
    }

    stages {
       stage('Clean Workspace') {
            steps {
                script {
                    deleteDir()
                }
            }
        }
        stage('Cleanup') {
            steps {
                script {
                    def buildDir = "/mnt/project"
                    if (fileExists(buildDir)) {
                        sh "rm -rf ${buildDir}"
                    }
                }
            }
        }
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/madhuriaws2/webapp.git', branch: 'master'
            }
        }
        stage('Build Project') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Post Build Actions') {
            steps {
                sh 'cp -r /mnt/project/target/WebApp.war /mnt/web-server/apache-tomcat-9.0.89/webapps'
                
            }
        }
    }	
  
}

