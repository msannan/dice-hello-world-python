pipeline {
   
  agent none
    stages 
	{
       	    stage('Build') 
	    {
		agent { docker 'python:2-alpine'} 
		
		steps {
			sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
		      }
      	     }

       	    stage('Test') 
	     {
           	 agent { docker 'qnib/pytest' }
            
		 steps {
			sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
		       }
       	     }
		
            stage('Deliver') 
	     {
		  agent { docker 'cdrx/pyinstaller-linux:python2' } 
		
		  steps {
			sh 'pyinstaller --onefile sources/add2vals.py' 
			}
		     
                   post 
		     {
               		 success {
			   	    archiveArtifacts 'dist/add2vals'
                      		 }
		     }
             }


        }
 }
