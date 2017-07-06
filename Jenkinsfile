#!groovy
@Library("Reform")
import uk.gov.hmcts.Ansible

def ansible = new Ansible(this, 'ccfr')

lock('fees-register-demo-deploy') {

  try {
    node {
      onMaster {
        stage('Deploy (Demo') {
          deleteDir()
          ansible.runDeployPlaybook('', 'demo')
        }
      }
    }
  } catch (err) {
    notifyBuildFailure channel: '#cc_tech'
    throw err
  }
}
