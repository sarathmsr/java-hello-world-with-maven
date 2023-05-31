pipeline{
    agent any

    tools {
         maven "mvn"
    }

    stages{
        stage('Test'){
            steps{
                   checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitcreds', url: 'git@github.com:sarathmsr/java-hello-world-with-maven.git']]])
                sh "mvn clean package"
            }
        }
    
	stage('dockerbuild'){
	    steps{
		    sh "docker build . -t smadavan/nodehello:${BUILD_NUMBER}"
            }
        }
	stage('docker push') {
	     steps {
		      script {
		      withDockerRegistry(credentialsId: 'dockerregistry') {
			      sh "docker push smadavan/nodehello:${BUILD_NUMBER}"
		       }
            }
	 }
    }
}
