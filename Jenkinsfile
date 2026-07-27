pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/jasonryu1991/ktcloudinfrajenkins.git', branch: 'main'
      }
    }
    stage('delivery and deployment using k8s') {
      steps {
        sh '''
        ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf get no"
        '''
      }
    }
  }
}
