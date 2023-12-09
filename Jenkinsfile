pipeline {
    agent any

   // tools {
        // Install the Maven version configured as "M3" and add it to the path.
       // maven "M3" is the tool that we will use to build this project is protected
   // }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/Geopell-Cloud/myfirstclassrepo.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                 bat "mvnw.cmd -Dmaven.test.failure.ignore=true clean package"
            }
	}
            stage('Test') {
		    steps {
                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                 bat "mvnw.cmd test"
            }
       }
       
       

// This is the beginning of the Amazon Fie Copy.



stage('Copy File to EC2') {
            steps {
                script {
                    // Replace placeholders with your actual values
                    def localFilePath = 'C:\\Users\\cmdch\\Documents\\Cloud Engineer Training\\something_light.txt'
                    def ec2Username = 'ec2-user'
                    def ec2IpAddress = '18.189.27.159'
                    def ec2KeyPath = 'C:\\Users\\cmdch\\Documents\\Cloud Engineer Training\\CloudTraining2023.pem'
                    def remoteDirectory = '/home/ec2-user/devops/'

                    // Use the scp command to copy the file
                    bat "winscp -i "${ec2KeyPath}" "${localFilePath}" ${ec2Username}@${ec2IpAddress}:${remoteDirectory}"
                }
            }
        }
       // This is the end of the Amazon File Copy.
          
    }	       
          post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
	}
