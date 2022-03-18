pipeline{

agent {label 'slave1'}

triggers {
       // poll repo every 2 minute for changes
       pollSCM('* * * * *')
   }

stages{
stage('scm'){
steps{
checkout([$class: 'GitSCM', branches: [[name: '*/feat01']], extensions: [], userRemoteConfigs: [[credentialsId: '4599f6fe-82d0-47e3-bd9c-c2959fe91a6b', url: 'https://github.com/test-satya/mavenrepo.git']]])
}
}      //scm stage end

stage('build'){
steps{
sh 'mvn package'
}
}   //build stage end

stage('sonar'){
steps{
withSonarQubeEnv('mysonarqube'){
sh 'mvn sonar:sonar'	
}
}
}  //build stage sonar end

stage('nexus'){
steps{
sh 'mvn deploy'
}
}  //nexus stage end

}        //stages end
}       //pipeline end
