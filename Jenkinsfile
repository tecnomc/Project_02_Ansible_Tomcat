pipeline { 
    agent any

    stages {
	
        stage('CLONE GITHUB CODE') {
            steps {
                echo 'In this stage code will be cloned'
                git branch: 'main', url: 'https://github.com/adarsh0331/Project_2.git'
            }
        }
		
        stage('BUILDING THE CODE') {
            steps {
                echo 'In this stage code will be built and mvn artifact will be generated'
                sh 'mvn clean install'
            }
        }		
		
        stage('DEPLOY WITH ANSIBLE') {
            steps {
                echo 'In this stage, Ansible will deploy the WAR file to Tomcat'
                sh '''
                    #ARTIFACT=$(ls target/*.war | head -n 1)
                    ARTIFACT=$WORKSPACE/target/devops-3.2.0.war
                    echo "Deploying artifact: $ARTIFACT"
                    ansible-playbook ansible/deploy_tomcat.yml --extra-vars "artifact=$ARTIFACT"
                '''
            }
        }
    }
}
