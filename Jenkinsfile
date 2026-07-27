pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/jasonryu1991/ktcloudinfrajenkins.git', branch: 'main'
      }
    }
    stage('Docker image build') {
      steps {
        sh 'docker build -t jasonryu1991/ktcloudinfra4:0727 .'        
      }
    }
    stage('Docker image push') {
      steps {
        sh 'echo "dckr_pat_3m8RUZ0lA9c9V5JIlR_5-LakoVA" | docker login -u jasonryu1991 --password-stdin'
        sh 'docker push jasonryu1991/ktcloudinfra4:0727'
      }
    }
    stage('delivery and deployment using k8s') {
      steps {
        sh '''
        ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf get no"
        ansible master -m copy -a "src=deploy.yml dest=/root/deploy.yml"
        ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf apply -f deploy.yml"
        ansible master -m shell -a "kubectl --kubeconfig=/etc/kubernetes/admin.conf get pod,deploy,svc"
        '''
      }
    }
  }
}
