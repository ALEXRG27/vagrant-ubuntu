
# Vagrant + Ansible Project

This project utilizes Vagrant to create and configure a virtual machine (VM) and Ansible for provisioning the VM with various software and tools. Below is a detailed description of the setup and the processes involved.

## Vagrant Configuration

The `Vagrantfile` configures a VM with the following specifications:

* **Base Box** : `bento/ubuntu-22.04` - This is an Ubuntu 22.04 LTS base image.
* **Port Forwarding** : Maps port 80 on the guest VM to port 1337 on the host machine.
* **Private Network** : Assigns a private IP address `172.17.177.12` to the VM.

### VM Definition

* **Controller** : A single VM named 'controller' is defined. This VM is provisioned using Ansible.

### Ansible Provisioning

The VM is provisioned using the `ansible_local` provisioner with the following parameters:

* **Playbook** : `setup_docker.yml`
* **Verbose** : Enabled for detailed output during provisioning.
* **Install** : Ensures Ansible is installed on the VM.
* **Limit** : Applies the playbook to all hosts in the inventory.
* **Inventory** : Uses the inventory file located at `inventory`.

## Ansible Playbook

The `setup_docker.yml` playbook installs and configures various packages and tools on the VM.

### Playbook Structure

* **Hosts** : The playbook is applied to all hosts.
* **Become** : Uses privilege escalation (sudo) to execute tasks.

### Variables

* **container_count** : Number of Docker containers to create (default: 4).
* **default_container_name** : Base name for Docker containers (default: `docker`).
* **default_container_image** : Docker image to use for containers (default: `ubuntu`).
* **default_container_command** : Command to run in the containers (default: `sleep 1d`).

### Tasks

1. **Install Aptitude** : Ensures `aptitude` package manager is installed and updated.
2. **Install Required System Packages** : Installs various system packages necessary for development and deployment.
3. **Install pytest** : Installs `pytest` using pip3.
4. **Download and Install nRF Command Line Tools** : Downloads and installs the nRF Command Line Tools package.
5. **Download and Extract GCC ARM Toolchain** : Downloads and extracts the GCC ARM toolchain to `/opt`.
6. **Copy SEGGER JTAG Tools** : Copies the SEGGER JTAG tools from the Vagrant host to the VM.
7. **Install SEGGER JTAG Tools** : Installs the SEGGER JTAG tools package.
8. **Install Docker Module for Python** : Installs the Docker module for Python using pip3.
9. **Pull Default Docker Image** : Pulls the default Docker image (`ubuntu`).
10. **Create Default Containers** : Creates the specified number of Docker containers using the default image and command.

## Usage

To set up the VM and provision it with the specified tools, follow these steps:

1. **Install Vagrant** : Ensure Vagrant is installed on your system.
2. **Install VirtualBox** : Ensure VirtualBox is installed as the provider for Vagrant.
3. **Navigate to Project Directory** : Open a terminal and navigate to the directory containing the `Vagrantfile`.
4. **Run Vagrant** : Execute `vagrant up` to create and provision the VM.
´´´
vagrant up
´´´
5. **Access the VM** : Once provisioning is complete, you can access the VM using SSH.
´´´
vagrant ssh controller
´´´
This setup ensures that the VM is ready for development with all the necessary tools installed and configured.
