- Add checks, everywhere, maybe even restructure for `set -e`
- `root` user might not be needed on the Proxmox host
- Should probably lock Ansible k3s repo to a known working commit and not just pull latest
- Just install libguestfs-tools automatically on Proxmox host (or maybe not)
- Terraform `main.tf` currently ignores: 
  - Disk stuff. Seems like Terraform is not discovering the disks of the clones properly?
  - qemu-img. Same here.
- The Terraform user is granted a lot of permissions. From a security perspective this should probably be looked at
