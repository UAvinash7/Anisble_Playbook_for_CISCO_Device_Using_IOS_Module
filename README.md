# Anisble_Playbook_for_CISCO_Device_Using_IOS_Module

Ansible playbook for running commands on cisco devices using ios module and sends mail notifications if errors are detected during command executions.  

Here is an Ansible playbook that uses the cisco.ios.ios_command module to run diagnostic commands on Cisco devices. It registers the output and triggers an email notification via the community.general.mail module if specific abnormalities (like interface errors) are detected.

Explanation - 
1. ios_command: Executes specified CLI commands on the target Cisco device.
2. register: Captures the command output into a variable (diag_output) for later analysis
3. set_fact with conditional: Evaluates the output. In this example, it searches for strings like "errors" or "CRC" within the returned text.
4. community.general.mail: Sends the alert. Note that delegate_to: localhost is used so the email is sent from the Ansible control node, not the Cisco device itself.
5. when: Ensures the email task only executes if the abnormalities_found condition is met.
6. Inventory: Ensure your Inventory file includes the necessary ansible_network_os=cisco.ios and connection credentials.
