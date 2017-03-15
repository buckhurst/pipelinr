pipeline {
    
   agent any

   stages {

       stage('Build') {
            steps {
               sh './build.sh'
               sh 'rm test.sh'
            }
       }
       stage('Unit tests') {
           steps {
           parallel slow: { node('master') { 
                        checkout scm
                        sh './test.sh 5' 
           } 
           },
                    fast: { node('master') { 
                        checkout scm
                        sh './test.sh 1' 
                    } }   
           }

        }
       stage('Acceptance tests') {
           steps { sh './acceptance.sh' }
       }
   }
}
