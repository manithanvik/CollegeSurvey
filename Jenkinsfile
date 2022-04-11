pipeline{
    agent any

    tools{
        maven 'maven'
        jdk 'java15'
    }

    stages{
        stage('mvn clean'){
            steps{
                bat  'mvn clean'
            }
        }

        stage('maven compile'){
            steps{
                bat 'mvn compile'
            }
        }

        stage('maven test'){
            steps{
                bat 'mvn test'
            }
        }

        stage('maven package'){
            steps{
                bat 'mvn package'
            }
        }

        stage('collect artifact'){
     steps{
     archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
     }
     }
     stage('deploy to artifactory')
     {
     steps{
     
     rtUpload (
    serverId: 'Jfrog',
    spec: '''{
          "files": [
            {
              "pattern": "target/*.jar",
              "target": "maven1"
            }
         ]
    }''',
    buildName: 'holyFrog',
    buildNumber: '1'
)
     }}

     stage('email notification'){
         steps{
             mail bcc: '',
          body: 'pipeline code executed successfully with out any build faliures',
           cc: '',
            from: '',
             replyTo: '', 
             subject: 'pipeline executed successfully', 
             to: 'mros47567@gmail.com'
         }
     }
    }

}
