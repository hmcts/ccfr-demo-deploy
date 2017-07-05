#!groovy
@Library("Reform")
import uk.gov.hmcts.Ansible

def ansible = new Ansible(this, 'ccfr')

lock('fees-register-demo-deploy') {

    stageWithNotification('Delete old stuff') {
        deleteDir()
    }

    onMaster {
        stageWithNotification('Deploy to Demo') {
            ansible.runDeployPlaybook(version, 'demo')
        }
    }
}

private stageWithNotification(String name, Closure body) {
    stage(name) {
        node {
            try {
                body()
            } catch (err) {
                notifyBuildFailure channel: '#cc_tech'
                throw err
            }
        }
    }
}
