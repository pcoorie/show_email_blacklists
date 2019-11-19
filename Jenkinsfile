#!groovy

ansiColor('xterm') {
  echo "TERM=${env.TERM}"
  // prints out TERM=xterm
}
pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Reading') {
            steps {
                echo 'Reading..'
                echo "You will view blacklist for ${params.ACCOUNT}"
            }
        }
        stage('Your Blacklist') {
            steps {
                echo 'Deploying....'
                sshPublisher(publishers: [sshPublisherDesc(configName: 'mail', transfers: [sshTransfer(excludes: '', execCommand: "python /opt/iRedAPD-2.4/tools/wblist_admin.py --account ${params.ACCOUNT} --list --blacklist", execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('Master Blacklist') {
            steps {
                echo 'Deploying....'
                sshPublisher(publishers: [sshPublisherDesc(configName: 'mail', transfers: [sshTransfer(excludes: '', execCommand: "python /opt/iRedAPD-2.4/tools/wblist_admin.py --list --blacklist", execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
