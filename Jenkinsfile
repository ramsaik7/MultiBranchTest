node {
// Get Artifactory server instance, defined in the Artifactory Plugin administration page.
    def server = Artifactory.server "artifactory-server-id"
    def buildInfo = Artifactory.newBuildInfo() 

// Project Dir
    def project_path = "01-Jenkins/petclinic-code"


stage('GitCheckOut') {
git branch: 'main', credentialsId: '01', url: 'https://github.com/amitvashisttech/devops301-mindtree-09-Jan-2021.git'
}



dir(project_path){

stage('Maven Clean') {
sh 'mvn clean'
}

stage('Maven Compile') {
sh 'mvn compile'
}

stage('Maven test') {
sh 'mvn test'
}

stage('Sonar-Code-Analysis'){
sh 'mvn sonar:sonar' 
}
stage('Maven pkg') {
sh 'mvn package'
}

stage('Build Managment') {
      def uploadSpec = """{
	 "files": [
	{
	"pattern": "**/*.war",
	"target": "devops301-petclinic-war"
        }
	]
	}"""
	server.upload spec: uploadSpec
 }


stage('Archive Artifacts') {
archive 'target/*.war'    
}
}


 
}
