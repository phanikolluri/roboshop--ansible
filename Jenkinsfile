pipeline {

  agent {
    node {
      label 'workstation'
    }
  }

  environment {
    SSH=credentials('SSH')
  }

  parameters {
      string(name: 'COMPONENT', defaultValue: '', description: 'Which Component to run the pipeline')
  }

  stages {
    stage('Ansible Playbook') {
      steps {
        sh '''
        HOST=$(echo ${COMPONENT} | tr [:lower:] [:upper:])
        ansible-playbook -i inv.roboshop roboshop.yml -e HOST=${HOST}  -e ROLE=${COMPONENT} -e ansible_user=${SSH_USR} -e ansible_password=${SSH_PSW}
        '''
      }
    }
  }

}