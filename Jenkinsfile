pipeline {
    agent any
    stages {
	    stage('Clean Start'){
        	steps{
            		script{
                        	try
                        	{
                           		bat("rd C:\\spring-petclinic /s /q")
                        	}catch(Exception e){}
                	 }
        	   }
	    }
            stage('Clone'){
	        steps{
			dir('C:\\')
			{
        		bat("""
		            git clone https://github.com/K1tan/spring-petclinic.git
		            """)
			}
		    }
	        }
	    stage('Build') {
            	steps {
                	bat ('C:\\spring-petclinic\\build.bat')
		}
            }
	    stage('Archive'){
                steps{
			zip zipFile: "${BUILD_NUMBER}.zip", archive:false, dir: 'target'
			archiveArtifacts artifacts: "${BUILD_NUMBER}.zip"
		}
	    }
	    stage('Deploy'){
		steps{
				script{
					try
					{
						bat("md C:\\Deploy\\")
					}catch(Exception e){}
				}
				unzip zipFile: "${BUILD_NUMBER}.zip", dir: 'C:\\Deploy'
			
		}
	   }
	}
}
