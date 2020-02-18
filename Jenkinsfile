node {
 try  {
 notify('Job Started') 


  stage('Git-Checkout') {
   git 'https://github.com/smbbasha/terraform.git'
  }
def project_path=""
 
 dir(project_path) {
    
  stage('Maven-Clean') {
   sh label: 'CLEAN', script: 'mvn clean'
  }
 } 
def project_terra="InstanceCreation"
dir(project_terra) {
   stage('Prod Deployment on AWS'){
   sh label: 'terraform', script: '/root/bin/terraform  init'
   sh label: 'terraform', script: '/root/bin/terraform  apply -input=false -auto-approve'
   }
}

 

notify('Job Completed')   
} catch (err) {
  notify("Error ${err}")
  currentBuild.result = 'FAILURE'
}
}


def notify(status){
    emailext (
    to: "mansoor4win@gmail.com",
    subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
     body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
    <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
        )
    }
