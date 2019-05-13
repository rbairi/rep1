pipeline {
    // agent { docker { image 'python:3.5.1' } }
    agent any
    stages {
        stage('build') {
            steps {
                // sh 'python --version; echo hello world;'
                sh """
                echo HELLO WORLD
                echo TESTING MULTILINE HELLO WORLD
                pwd
                ls -l
                echo BEFORE SSH_PUBLISHER
                """
                
                // Start of sshPublisher
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            // Only configured hosts in Jenkins can be given for "configName" parameter
                            // Contact DevOps to add your required hosts to Jenkins configuration before
                            // specifing the value for "configName"
                            configName: 'test_host', 
                            
                            // STEP 1 (of 2)
                            // TRANSFER FILES TO THE TARGET HOST (host to deploy)
                            // Change the value for "remoteDirectory" to match the folder into which you want to copy files
                            transfers: [
                                sshTransfer(
                                    cleanRemote: false, 
                                    excludes: '', 
                                    execCommand: '', 
                                    execTimeout: 120000, 
                                    flatten: false, 
                                    makeEmptyDirs: false, 
                                    noDefaultExcludes: false, 
                                    patternSeparator: '[, ]+', 
                                    remoteDirectory: 'from_jenkins_pipeline', 
                                    remoteDirectorySDF: false, 
                                    removePrefix: '', 
                                    sourceFiles: '**/*'
                                ),
                                
                                // STEP 2 (of 2)
                                // Execute the deployment script that runs after transferring files. 
                                sshTransfer(
                                    cleanRemote: false,
                                    excludes: '',
                                    execCommand:  '''
echo \'This is on the test_host: \' `hostname`
echo \'PWD: \' `pwd`
echo \'EXECUTING ./deploy.sh\'
./deploy.sh
echo \'DONE\'
''',
                                    execTimeout: 120000,
                                    flatten: false,
                                    makeEmptyDirs: false,
                                    noDefaultExcludes: false,
                                    patternSeparator: '[, ]+',
                                    remoteDirectory: '',
                                    remoteDirectorySDF: false,
                                    removePrefix: '',
                                    sourceFiles: ''
                                )
                            ], 
                            usePromotionTimestamp: false, 
                            useWorkspaceInPromotion: false, 
                            verbose: false
                        )
                    ]
                )
                // END of sshPublisher
                
                sh 'echo AFTER SSH_PUBLISHER;'
                
            }
        }
    }
}
