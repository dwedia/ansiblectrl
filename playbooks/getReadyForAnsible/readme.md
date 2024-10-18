# Playbook to get a target server ready for ansible management.

### Why?
Getting a server ready for use with ansible management can be a tedious task. The user needs to be created, it needs to be given the correct sudo rights, the public key needs to be copied over, and lastly root ssh login needs to be disabled as fast as possible.

To make this easier, when making servers, especially shortlived test servers, I have created this playbook that does all that for me.

### Requirements
To use this playbook, root ssh access with password needs to be enabled for the run. The last task of the playbook disables root ssh login.  
NOTE: It also disables password based login altogether.

### Playbook output

```bash
$ ansible-playbook -i <target IP>, playbooks/getReadyForAnsible/getReadyForAnsible.yml -k
SSH password: 
Enter the user name:: <enter username here>
Enter the user password:: 

PLAY [get target ready for ansible] ***********************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************
ok: [<target IP>]

TASK [Create user] ****************************************************************************************************************************************
changed: [<target IP>]

TASK [Create drop-in sudoers file] ************************************************************************************************************************
changed: [<target IP>]

TASK [add line in sudoers file] ***************************************************************************************************************************
ok: [<target IP>]

TASK [create .ssh if it does not exist] *******************************************************************************************************************
ok: [<target IP>]

TASK [copy authorized_keys file] **************************************************************************************************************************
changed: [<target IP>]

TASK [close down root ssh login] **************************************************************************************************************************
changed: [<target IP>] => (item={'regex': '^#PermitRootLogin', 'line': 'PermitRootLogin no'})
ok: [<target IP>] => (item={'regex': '^#PubkeyAuthentication yes', 'line': 'PubkeyAuthentication yes'})
changed: [<target IP>] => (item={'regex': '^#PasswordAuthentication', 'line': 'PasswordAuthentication no'})
ok: [<target IP>] => (item={'regex': '^#PermitEmptyPasswords no', 'line': 'PermitEmptyPasswords no'})

RUNNING HANDLER [restart sshd after editing sshd_config] **************************************************************************************************
changed: [<target IP>]

PLAY RECAP ************************************************************************************************************************************************
<target IP>                 : ok=8    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

### Test that it works

Once we have run the above playbook, we can use an adhoc ansible command to test that its working as intended.
```bash
[ansiblewizard@wizardstower ansiblectrl]$ ansible all -i <target IP>, -m ping

PLAY [Ansible Ad-Hoc] *************************************************************************************************************************************

TASK [ping] ***********************************************************************************************************************************************
ok: [<target IP>]

PLAY RECAP ************************************************************************************************************************************************
<target IP>                 : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```