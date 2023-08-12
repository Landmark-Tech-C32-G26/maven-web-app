Jenkinsfile1: declarative
*https://github.com/LandmakTechnology/maven-web-app*

pipeline{
  agent any  
  tools {
    maven "maven3.8.2"
  }
  //options {}  
  //triggers {}
  stages{
    stage('1clone'){
      steps{
        sh "echo ready to automate build"
        git branch: 'development', credentialsId: 'gitHubCredentials', url: 'https://github.com/LandmakTechnology/maven-web-app'
        sh "echo latest application version collected from SCM"
      }   
    }
    stage('2build'){
      steps{
        sh "echo build process starts "
        sh "mvn clean package"
        sh "echo build process ends"
      }
    }
 
    stage('3review'){
      steps{
        sh "echo CodeQuality review  starts "
        sh "mvn sonar:sonar"
        sh "echo CodeQuality review ends"
      }
    }      
    stage('4UploadArtifacts'){
      steps{
        sh "mvn deploy"
        sh "echo build and release job completed successfully"
      }     
    }
    stage('5deployment'){
      steps{
        deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://54.166.85.32:8177/')], contextPath: null, war: 'target/*war'
        sh "echo deployment to production completed successfully"
      }       
    }
  }
  post{
    failure{
         emailext body: '''Hi Team,
Build failed
Landmark Technologies''', recipientProviders: [developers(), contributor()], subject: 'build status', to: 'developers'

    }
    success{
         emailext body: '''Hi Team,
Build succeeded
Landmark Technologies''', recipientProviders: [developers(), contributor()], subject: 'build status', to: 'developers'

    }
    always{
         emailext body: '''Hi Team,
Build status
Landmark Technologies''', recipientProviders: [developers(), contributor()], subject: 'build status', to: 'developers'

    }
  }
  
}

Jenkinsfile1: scripted

node{
  def mavenHome: tool name "maven3.8.2"
  stage('1'){}
  stage('2'){}
  stage('3'){}
  stage('14'){}
}


 maven "maven3.8.2"



node{
  def mavenHome = tool name: 'maven3.8.2'
  stage('1Clone'){
    //git "https://github.com/LandmakTechnology/maven-web-app"
    git branch: 'development', credentialsId: 'gitHubCredentials', url: 'https://github.com/LandmakTechnology/maven-web-app'
  }
  stage('2Test+build'){
    sh "${mavenHome}/bin/mvn clean package"
  }
  stage('SonarQube'){
    sh "${mavenHome}/bin/mvn sonar:sonar"
  }
  stage('4UploadArtifacts'){
    sh "${mavenHome}/bin/mvn deploy"
  }
  stage('5Deploy'){
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://54.166.85.32:8177/')], contextPath: null, war: 'target/*war'
  }
  stage('6Notification'){
    emailext body: '''Hi Team,
Build status
Landmark Technologies''', recipientProviders: [developers(), contributor()], subject: 'build status', to: 'developers'
  }
}


node{
  def mavenHome = tool name: 'maven3.8.2'
  stage('1Clone'){
    git 'https://github.com/LandmakTechnology/maven-web-application'
  }
  stage('2Test+build'){
    sh "${mavenHome}/bin/mvn clean package"
  }
/*
  stage('SonarQube'){
    sh "${mavenHome}/bin/mvn sonar:sonar"
  }
  stage('4UploadArtifacts'){
    sh "${mavenHome}/bin/mvn deploy"
  }
  stage('5Deploy'){
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://54.166.85.32:8177/')], contextPath: null, war: 'target/*war'
  }
  stage('6Notification'){
    emailext body: '''Hi Team,
Build status
Landmark Technologies''', recipientProviders: [developers(), contributor()], subject: 'build status', to: 'developers'
  }
  */
}
