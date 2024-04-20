pipleline {
    agent any 
    tool {
        maven 'maven3.9.6'
    }
    stages {
        stage("Build jar") {
            echo "Building jar file"
            sh 'mvn clean package'
        }
        stage("Build docker image and push") {
            echo "building the docker image..."
            withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                sh 'docker image build -t navr24396/java-maven-app:pipeline1.0 .'
                sh "echo $PASS | docker login -u $USER --password-stdin"
                sh 'docker image push navr24396/java-maven-app:pipeline1.0 .'
            }
        }
        stage("Deploy the application") {
            echo "Deploying the application"
        }
    }
}
