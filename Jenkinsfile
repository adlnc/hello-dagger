#!/usr/bin/env groovy

pipeline {
  agent {
    kubernetes {
      yaml '''
apiVersion: v1
kind: Pod
metadata:
  name: jslv-dagger
spec:
  containers:
    - name: dagger
      image: "adlnc/dagger-jenkins-agent:test"
      imagePullPolicy: Always
      command:
        - sh
      tty: true
      volumeMounts:
        - name: docker-registry-config
          mountPath: /dagger/.docker
  volumes:
    - name: docker-registry-config
      configMap:
        name: docker-registry-config
'''
      retries 2
    }
  }
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
