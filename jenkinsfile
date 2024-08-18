pipeline{
    
    agent any
    
    tools{
        maven 'mymaven'
    }
    
    stages{
        stage('Checkout Code')
        {
            steps{
                git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
            }
        }
        
         stage('Code Review')
        {
            steps{
                
                sh 'mvn pmd:pmd'
                
            }
            post{
                // various post actions
                 always{
                    echo "This is post build steps"
                }
                
                unstable{
                   echo "The number of warnings are more than 15, build is unstable" 
                }
                success{
                    
                    recordIssues sourceCodeRetention: 'LAST_BUILD', tools: [pmdParser(pattern: '**/pmd.xml')]
                    
                }
               
            }
        }
        
         stage('Code Test')
        {
            steps{
                
                sh 'mvn test'
                
            }
        }
        
         stage('Code Build')
        {
            steps{
                
                sh 'mvn package'
                
            }
        }
    }
       
}
