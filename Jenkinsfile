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
            sh "docker login -u ${dockerHubUser} -p ${dockerHubPassword}"
            sh "docker push registry.cn-hangzhou.aliyuncs.com/bigops-repo1/bigops/jenkins-demo:latest"
        }
    }
    stage('Deploy') {
        echo "5. Deploy Stage"
      
       
    }
}
