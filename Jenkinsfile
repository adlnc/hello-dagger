#!/usr/bin/env groovy
podTemplate {
    node(POD_LABEL) {
      environment {
        DH_CREDS = credentials('3f3f1cdb-c931-4993-a2df-59bdf30c48b7')
      }
      stages {
        stage('verify installation') {
          steps {
            sh '''
            dagger version
            docker version
            '''
          }
        }
      }
    }
}
