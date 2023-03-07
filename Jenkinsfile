pipeline {
    agent {
        kubernetes {
            defaultContainer 'dagger'
            yaml '''
            kind: Pod
            spec:
              containers:
                - name: dagger
                  image: adlnc/dagger-jenkins-agent:test
                  imagePullPolicy: Always
                  command:
                    - sh
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