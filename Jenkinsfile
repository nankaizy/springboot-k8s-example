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
   
    stage('Build') {
        echo "3.Build Docker Image Stage"
        sh "pwd"
        sh "docker build -t jenkins-demo:latest ."
    }
    stage('Push') {
        echo "4.Push Docker Image Stage"
        withCredentials([usernamePassword(credentialsId: 'AliRegistry', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
            
            sh "docker login -u ${dockerHubUser} -p ${dockerHubPassword} registry.cn-hangzhou.aliyuncs.com"
            sh "docker push registry.cn-hangzhou.aliyuncs.com/bigops-repo1/jenkins-demo:latest"
        }
    }
    stage('Deploy') {
      
        echo "5. Deploy Stage"
		withKubeConfig([credentialsId: 'eb583be7-8a4a-404f-8d04-d2b65a32e607', serverUrl: 'https://172.31.51.143:6443']) {
      sh 'kubectl apply -f deployment/deployment.yaml'
    }
      
       
    }
}
