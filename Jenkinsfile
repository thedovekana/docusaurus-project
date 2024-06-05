pipeline {
    agent any

    stages {
        stage('SCM Checkout') {
            steps {
                git 'https://github.com/thedovekana/docusaurus-project.git'
            }
        }
        stage('Build') {
            steps {
                sh '/usr/bin/npm install '
                sh '/usr/bin/npm run build'
                sh 'mv build.tar.gz build.tar.gz_$(date +"%Y-%m-%d")'
                sh 'tar -czvf build.tar.gz build'
            }
        }
        stage('Copy Artifact to Ansible server') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansiblemaster', sshCredentials: [encryptedPassphrase: '{AQAAABAAAAAQM7/oZqkpef6k7MxTl/3oj6Oibg2gV67waRVXYIcfGnQ=}', key: '', keyPath: '', username: 'vagrant'], transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo rm -Rf *.gz *.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//home//vagrant', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansiblemaster', sshCredentials: [encryptedPassphrase: '{AQAAABAAAAAQcFydTQTWGvC/NyTg5OBFmce5ABAUS0xA8fdl9EHQEkY=}', key: '', keyPath: '', username: 'vagrant'], transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//home//vagrant', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '*.gz, *.yml')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                
                
            }
        }
        stage('Deploy artifact to the webserver') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansiblemaster', sshCredentials: [encryptedPassphrase: '{AQAAABAAAAAQ8YGhTNfGu+KPcPI5vJQTjWKUoxNgPvHJu2wyDC3pQO8=}', key: '', keyPath: '', username: 'vagrant'], transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook docusaurus-deploy.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//home//vagrant', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                
                
            }
        }
    }
}
