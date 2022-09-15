 //def appName='E2E_App'
    def appName='App_2'
    def snapName=''
    //def deployName = 'TEST'
    //def deployName ='PerfApp91_dep__1'	
    def deployName ='Dep_1'
    def exportFormat ='json'
    def configFilePath = "fileB"
    def fileNamePrefix ='exported_file_'
    def fullFileName="${appName}-${deployName}-${currentBuild.number}.${exportFormat}"
   // def fullFileName="Comp_2"
    def changeSetId=""
    def snapshotName=""
    def exporterName ='returnAllData' 

    // def namePath ="E2E/pipelineUpload/${currentBuild.number}"
   def namePath ="Comp_2"
  // def namePath ="Comp_1/${JOB_NAME}/${currentBuild.number}"
//def namePath ="App_2/components/Comp_1${JOB_NAME}/"
pipeline {
    agent any
    stages {
     
     stage('E2E_Pipeline2_1') {
            steps {
                echo "Running E2E_Pipeline2_1..........."
                echo "MY_PARAM=${env.MY_PARAM}"
            }
        }
     
        stage('Clone repository') {               
           steps{
                // checkout scm
                git branch: 'main', url: 'https://github.com/rajkumat01/samplejava2_1'
           }
        }     
        stage('Upload JSON'){
            steps{
                script{
                    sh "echo validating configuration file ${configFilePath}.${exportFormat}"
                    echo "name path ::::: ${namePath}"
                    changeSetId = snDevOpsConfigUpload(applicationName:"${appName}",target:'component',namePath:"${namePath}", configFile:"fileB.json", autoCommit:true,autoValidate:true,dataFormat:"${exportFormat}")
                    // snDevOpsConfigUpload(applicationName:"${appName}",target:'deployable',namePath:"${namePath}", fileName:"deployable", autoCommit:'true',autoValidate:'true',dataFormat:"${exportFormat}",changesetNumber:"${changeSetId}", deployableName:"${deployName}")
                    echo "validation result $changeSetId"
                }
            }
        }
        stage("Committing the changeset"){
            steps{
                script{
                    echo "Change set registration for ${changeSetId}"
                    changeSetRegResult = snDevOpsConfigRegisterPipeline(changesetNumber:"${changeSetId}")
                    echo "change set registration set result ${changeSetRegResult}"
                }
            }
        }
    }
}
