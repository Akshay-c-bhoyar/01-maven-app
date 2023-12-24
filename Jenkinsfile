pipeline {
    agent any
    environment {
         path="$PATH:/opt/apache-maven-3.8.8/bin"
    }    
    stages{
        stage('Getcode'){
            steps{
                git branch: 'main', url: 'https://github.com/Akshay-c-bhoyar/01-maven-app.git'    
            }   
        }
        stage('build'){
            steps{
                sh'mvn clean package'
            }
        }
        // stage('sonarqube analysis'){
        //     steps{
        //         withsonarcube Env('sonar-server-7.8'){
        //         sh "sonar:sonar-7.8"
        //         }
        //     } 
        // }
        stage('Deploy'){
            steps{
		sshagent(['Tomcat-server-agent']){                                                     
		     sh'scp -o strictHostkeychecking=no target/01-maven-app.war ec2-user@34.219.239.144:/home/ec2-user/apachetomcat-9.0.63/webapp'
                }              
            }
        }
    }
    post{
             always{
                 mail to:"bhoyar.akshay160@gmail.com",
                 subject:"Test Email",
                 body:"Test"
	         }
 	}		 
	
    
}