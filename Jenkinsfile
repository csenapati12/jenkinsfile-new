def loadProperties() {
    node {
        checkout scm
        properties = new Properties()
        File propertiesFile = new File("${workspace}/build.properties")
        properties.load(propertiesFile.newDataInputStream())
        echo "Immediate one ${properties.repo}"
    }
}

pipeline {
    agent none

    stages {

        stage ('prepare') {
            agent any

            steps {
                script {
                    loadProperties()
                    echo "Later one ${properties.branch}"
                }
            }
        }
        stage('Build') {

            agent { label 'master'  }

            steps {
                // works fine. properties is available everywhere
                echo properties.branch
            }

        }
    }
}

	 
