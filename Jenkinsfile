pipeline {
	agent any 
	stages {
    stage(‘Update’) {
	steps {
        sh "sudo rm -rf webserver/ "
	}
	}
	stage (‘install’) {
	steps {
		sh "sudo yum install npm -y"
		sh "sudo npm install -g create-react-app@3.4.1"
	}
	}
    stage (‘Initialization’) {
	steps {
		sh "npm init react-app webserver --use-npm"
	}
    	}
    stage (‘Build’) {
	steps {
		sh "cd webserver && npm run build"
		sh "sudo cp -R /home/centos/project/docker-compose.yml  /var/lib/jenkins/workspace/SSR/webserver/ && sudo cp -R /home/centos/project/Dockerfile.prod  /var/lib/jenkins/workspace/SSR/webserver/"
	}
	}

        stage (‘Deploy’) {
	steps {
		
		sh	"cd webserver && docker build -t web-server:latest -f /var/lib/jenkins/workspace/SSR/webserver/Dockerfile.prod . " 
		sh	"docker tag web-server:latest 963750697977.dkr.ecr.us-east-1.amazonaws.com/web-server:latest"
        sh  "docker push 963750697977.dkr.ecr.us-east-1.amazonaws.com/web-server:latest"

        }
	}
}
}
