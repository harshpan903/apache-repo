# Integrating git,ansible and apache using pipeline
pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                git 'https://github.com/harshpan903/apache-repo.git'
            }
        }
        
        stage('Copy index.html file to jenkins'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkins', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'rsync -avh https://github.com/harshpan903/apache-repo.git      ', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        
        stage('copy index.html file from jenkins to ansible '){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'jenkins', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'rsync -avh  /var/lib/jenkins/workspace/apache-project/*.html   root@172.31.65.137:/opt/index.html  ', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
              }
         }
         
         stage('copy index.html file from ansible to apache '){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /sourcecode/abc.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
              }
         }
       
        }
    }



