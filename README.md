## Description
Simple script that attempts to install a k3s cluster together with kubernetes-dashboard in your Proxmox environment.

## FAQ
- How many different environments has this been tested on as of 2023-06-22?  
  1
- Will this work for me right out off the box?  
  Maybe, but probably not
- How many edgecases have you covered?  
  Maybe 5 out of 30000
- Should I use this to set up my production environment?  
  No
- Will the script stop on errors?  
  No, spam ctrl+c
- What will the script do to the machine running it?
  - Generate SSH-keypair `~/.ssh/id_rsa_lab_kubernetes_<your_ansible_clustername>`
  - Start your SSH-agent and add above key to it
  - Create Terraform dir and files where your are running the script
  - Git clone Ansible k3s playbooks where you are running the script
  - Create maifests dir and files where you are running the script
  - Create kube dir and files under `~/.kube/`

## Prerequisites
- Machine running script:
  - Passwordless SSH access to Proxmox host with `root` user  
    (this must work from your terminal: `ssh root@<proxmox-ip>`)
  - Terraform: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
  - Ansible: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
  - kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
  - jq, git: `sudo apt update && sudo apt install -y jq git`
- Proxmox host:
  - Internet access
  - libguestfs-tools: `apt update && apt install -y libguestfs-tools`

## Procedure
1. Place `deploy` and `vars.conf` in an empty folder
2. Edit variables in `vars.conf`
3. Run with `./deploy`  
   The script will output more instructions once it finishes

- The script can be used to add and remove nodes by simply editing `vars.conf` and running it again.  
  Cluster downtime when doing this is expected.
- The script overwrites Terraform and Ansible configuration each run based off `vars.conf`  
  This means that any template changes outside `vars.conf` must be done in `deploy`  
  Or just ditch the script entierly and configure Terraform and Ansible manually
