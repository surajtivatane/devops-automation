pipeline {
    agent any
tools{

    maven 'maven'
    
            }
            stages{
        stage('Build Maven'){
            steps{
             checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/surajtivatane/devops-automation']])
             sh 'mvn clean install'
        }
    }
    stage('OWASP Scan') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ ', odcInstallation: 'DC'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
    stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t surajdocker321/devops-integration .'
}
}
}
                    stage('Push image to Hub'){
                      steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                       sh 'docker login -u surajdocker321 -p ${dockerhubpwd}'

}
                   sh 'docker push surajdocker321/devops-integration' 
   
}
}
}
}


}
