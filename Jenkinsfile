pipeline
{
 agent any
 stages{

     stage('scm checkout')
     {steps {  git branch: 'master', url: 'https://github.com/prakashk0301/maven-project' }    }

     stage ('code Build')
     { steps {  withMaven(jdk: 'JDK_HOME', maven: 'Maven_Home') 
          { sh 'mvn clean package' }  }  }
  
    stage (' send artifacts from jenkins workspace to ansible controllers playbook folder')
  { steps { sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible-controller', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook ci-cd-playbook.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//etc//ansible//playbooks', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)]) }
  
  }}}
