pipeline {
agent any
//triggers {
//cron('*/4 * * * *')
//}
  environment {
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "localhost:8081/Nexus"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "Releases"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "admin:admin"
    }
stages{
 stage('clone git'){
    steps {
    echo "Getting Project from Git";
    git branch:"main",url:"https://github.com/MarouaMad/javajenkinsdevops.git";
    
    }
 
 }

 stage('Verificationdu version Maven'){
   steps {
      sh "mvn --version"
   }
 }
 
 stage("supprimer le contenu du dossier target"){
   steps {
     script{
     //this step attempts to clean the files and directories generated by Maven during its build
     
     sh "mvn clean"
     }
   
   }
 
 }
 
 stage('Creation livrable'){
   steps {
   sh "mvn package -DskipTests=true"  
  /* apres dans le terminal ls /var/lib/jenkins/workspace/javapipeline-24-06/target/ pour voir le build fichier .jar */
  // sh "mvn package"  
   }
 
 }
 
// stage("Lancement des tests unitaires"){
  // steps {
   //  sh "mvn test"
// }
 
// } 
 
stage('Jacoco Build'){
          steps{
            step([$class: 'JacocoPublisher', 
            execPattern: 'target/*.exec',
            classPattern: 'target/classes',
            sourcePattern: 'src/main/java',
            exclusionPattern: 'src/test*'
            ])
          }
        }
 
// stage("Sonar") {
         // steps {

         //   sh "mvn sonar:sonar \
//  "-Dsonar.projectKey=test2023" \
//  "-Dsonar.login=squ_589d5c5b31e5e92f8f4338957d7bd0ee16969bdc""
      //    }
     //   }
 stage('Deploiement dans nexus ') {
     		 steps{
                          
  			sh "mvn deploy" }
                }
}

}
