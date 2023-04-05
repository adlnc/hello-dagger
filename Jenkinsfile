#!/usr/bin/env groovy

pipeline {
  agent { 
    kubernetes {
      yaml '''
        kind: Pod
        apiVersion: v1
        metadata:
          name: jslv-dagger
        spec:
          containers:
          - name: jslv-dagger
            image: adlnc/dagger-jenkins-agent:test
            imagePullPolicy: Always
            command:
            - sleep
            args:
            - 99d
            volumeMounts:
              - name: docker-registry-config
                mountPath: /dagger/.docker
          volumes:
            - name: docker-registry-config
              configMap:
                name: docker-registry-config
      '''
    }
  }
    // node("jslv-dagger") {
  environment {
    DH_CREDS = credentials('3f3f1cdb-c931-4993-a2df-59bdf30c48b7')
  }
  stages {
    stage('verify installation') {
      steps {
        container('jslv-dagger'){
          sh '''
          dagger version
          docker version
          '''
        }
      }
    }
  }
    // }
}
