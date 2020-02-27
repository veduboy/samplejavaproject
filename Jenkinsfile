node {
    
 def mvn = tool (name: 'maven 3.6', type: 'maven')
   
stage('CleanWorkspace') {
        cleanWs()
    }
 stage('SCM Checkout'){
 
	git branch: 'master', 
	url: 'https://github.com/opstree/spring3hibernate'
  }
   
stage('Mvn Package'){
	   // Build using maven
	   sh "mvn -f /var/lib/jenkins/workspace/tomcatwardeploy/pom.xml clean package"
      // sh "${mvn} -f /var/lib/jenkins/workspace/tomcatwardeploy/pom.xml clean compile"
  }

sshPublisher(
  continueOnError: false, failOnError: true,
  publishers: [sshPublisherDesc(
                  configName: 'host1', transfers:
                     [sshTransfer(
                        cleanRemote: false, 
                        excludes: '',
                        execCommand: '',
                        execTimeout: 120000, 
                        flatten: false, 
                        makeEmptyDirs: false,
                        noDefaultExcludes: false,
                        patternSeparator: '[, ]+',
                        remoteDirectory: '//opt/tomcat/webapps/', 
                        remoteDirectorySDF: false, 
                        removePrefix: '', 
                        sourceFiles: 'target/*.war')], 
                        usePromotionTimestamp: false, 
                        useWorkspaceInPromotion: false, 
                        verbose: false)
            ])
    
}
