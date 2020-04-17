import java.text.SimpleDateFormat;

properties([
    parameters([string(name: 'K8S_token', defaultValue: 'suebsgop1', description: 'k8s cluster login token'),
                string(name: 'ENABLE_BUILD', defaultValue: 'true', description: 'build docker image'),
                string(name: 'ENABLE_PUBLISH', defaultValue: 'true', description: 'push docker image'),
                string(name: 'ENABLE_DEPLOY', defaultValue: 'false', description: 'deploy image to OC'),
                string(name: 'ENABLE_TAGGING', defaultValue: 'false', description: 'tag back SCM')])
])

node ('master') {

    stage('Prepare') {
        echo "1.Prepare Stage"
        checkout scm
        
    }
   
  
    stage('Deploy') {
      
        echo "5. Deploy Stage"
		withKubeConfig([credentialsId: 'eb583be7-8a4a-404f-8d04-d2b65a32e607', serverUrl: 'https://172.31.51.143:6443']) {
      sh 'kubectl apply -f deployment/service.yaml'
    }
      
       
    }
}
