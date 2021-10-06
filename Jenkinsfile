def POM_ARTIFACTID
def POM_VERSION

node {
    
    environment {
     //  pom = readMavenPom file: 'pom.xml'
      // POM_VERSION = pom.version
    //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
    //POM_ARTIFACTID = readMavenPom().getArtifactId()
    // POM_VERSION = readMavenPom().getVersion()
    //def version = sh script: 'mvn help:evaluate -Dexpression=project.version -q -DforceStdout', returnStdout: true
    
    }

    stage('Checkout SCM'){
            
       git 'https://github.com/vveereshvsh/Jenkins_Assigment.git'
       // echo "${POM_ARTIFACTID}" 
       //    echo "${POM_VERSION}"
       //def version = sh script: 'mvn help:evaluate -Dexpression=project.version -q -DforceStdout', returnStdout: true
       pom = readMavenPom file: 'pom.xml'
       POM_VERSION = pom.version
       POM_ARTIFACTID = pom.artifactId
       echo "$POM_VERSION"
       echo "$POM_ARTIFACTID"
    }
      
    stage(" Build  ${POM_ARTIFACTID} and  ${POM_VERSION}") {
        def mvn_version = 'maven'
        withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ) {
            sh """export PATH=$PATH:/opt/maven/bin
               mvn clean package"""
        }
        echo "${currentBuild.currentResult}"
            //tool name: 'maven', type: 'maven'
            // sh 'mvn package'
    /*  def userInput = true
        def didTimeout = false
        try {    
            if ("${currentBuild.currentResult}" == "SUCCESS" ) 
            {
               timeout(time: 5, unit: 'MINUTES') { // change to a convenient timeout for you
               userInput = input(message: "Awaiting approval for deploying $POM_ARTIFACTID and $POM_VERSION. Are you ready to deploy?", parameters: [
               [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']
               ])
            }
        }
        }
        catch(err) { // timeout reached or input false
        def user = err.getCauses()[0].getUser()
        if('SYSTEM' == user.toString()) { // SYSTEM means timeout.
               didTimeout = true
        } else {
              userInput = false
              echo "Aborted by: [${user}]"
        }
} */
    }  
        stage("Awaiting for Approval for ${POM_ARTIFACTID} and  ${POM_VERSION}"){
        
        def userInput = true
        def didTimeout = false
        try {    
            if ("${currentBuild.currentResult}" == "SUCCESS" ) 
            {
               timeout(time: 5, unit: 'MINUTES') { // change to a convenient timeout for you
               userInput = input(message: "Awaiting approval for deploying $POM_ARTIFACTID and $POM_VERSION. Are you ready to deploy?", parameters: [
               [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']
               ])
            }
        }
        }
        catch(err) 
        { // timeout reached or input false
        def user = err.getCauses()[0].getUser()
        if('SYSTEM' == user.toString()) { // SYSTEM means timeout.
               didTimeout = true
        } else {
              userInput = false
              echo "Aborted by: [${user}]"
        }
    }
}

    stage("Deploying ${POM_ARTIFACTID} and  ${POM_VERSION}"){
       // sh 'sudo ansible-playbook -u devopsdemo deploy.yml'
     sshagent (credentials: ['SSH-tomcat']) {
       sh 'pwd'
       sh 'scp target/JenkinsAssignment.war devopsuser@34.93.180.28:/opt/tomcat/apache-tomcat-9.0.54/webapps/'
    }
}
    stage('Execute Tests'){
            
           sh "sleep 10"
            
           sh label: '', script: ''' URL="http://35.222.221.179:8080/JenkinsAssignment/"

      # store the whole response with the status at the and
      HTTP_RESPONSE=$(curl --silent --write-out "HTTPSTATUS:%{http_code}" -X POST $URL)

      # extract the body
      #HTTP_BODY=$(echo $HTTP_RESPONSE | sed -e \'s/HTTPSTATUS\\:.*//g\')

      # extract the status
      #HTTP_STATUS=$(echo $HTTP_RESPONSE | tr -d \'\\n\' | sed -e \'s/.*HTTPSTATUS://\')

      # print the body
      echo "$HTTP_RESPONSE"'''

      //sh "HTTP_RESPONSE=\$(curl http://35.222.221.179:8080/JenkinsAssignment/)"
      //    sh "echo ${HTTP_RESPONSE}"
      }
       
}
