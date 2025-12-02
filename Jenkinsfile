pipeline {          
    agent any         
    
    stages {  
        stage('Git Checkout') {
            steps {
               // git branch: 'sbomMaven', credentialsId: 'ssh_global_sep15_v_ID', url: 'git@github.com:agilitydelivered/ad-jenkins-qa-python.git'   
                git branch: 'sbomMaven', credentialsId: ' ssh_prod_global_v_oct10_ID', url: 'git@github.com:agilitydelivered/ad-jenkins-qa-python.git' 
               
            }
        }
        
        stage('Build') {
            steps {
                sh '''
                    sudo apt-get update -y
                    sudo apt-get install maven -y
                    mvn clean verify -Dmaven.test.skip=true  
                                                   
                '''
                
            }
        }
    }
    
    post {
        always {
            script {
                emailext(
                    subject: "pipeline-java-transitive-dependency",
                    body: '${JELLY_SCRIPT, template="ad_default_template"}',
                    mimeType: 'text/html',
                    to: 'jeya.veronica@agilitydelivered.com',
                    )
            }
        }
    }
}
