# Openstack Instance Ansible

This Ansible playbook aims to make provisioning multiple instances to Openstack a breeze. By specifing a list of instances to create in `vars.yml`, a user can automatically provision or delete the specified instances. An Ansible inventory file (`inventory.ini`) will automatically be created and any ssh keys added to the `files/keys` directory will also automatically be uploaded to Openstack.

This playbook can also be directly imported by other playbooks or used as a starting point when deploying and configuring services. Because of this, it brings a great deal of utility to the Gray team effort. When this playbook is combined with others, essentially, the entire competition can be repeatedly and consistently deployed and redeployed.

Features:
  - SSH Key Management
  - Instance Deployment

## Installation

This playbook requires a few steps in order to be installed.

1. First, create a new Python virtual environment inside of the project directory:

```bash
python3 -m venv ./venv
```

2. The newly created environment can then be activated via:

```bash
source venv/bin/activate
```

3. Next, install the required Python packages:

```bash
pip3 install -r requirements.txt
```

4. Afterwards, install the required Ansible Galaxy roles:

```bash
ansible-galaxy install -r requirements.yml
```

5. Once done, download your OpenStack RC File and move it to the project directory

6. Next, execute the file to load its environment variables:

```bash
source cdt-ech-openrc.sh # The exact file name will differ
```

*Make sure to input your Openstack password correctly. This is used for authentication in the Ansible playbook.*

## Configuration

### SSH Keys

In order to upload public keys to Openstack, simply drop them into the `files/keys` directory. Remember, any keys used in an instance must be available to Ansible if testing connectivity or using another playbook afterwards.

### Config File

The heart of the user options is inside of the `vars.yml` file. An example is already given in the file, however, this table can be used as a quick reference for the available options.

| Value        | Default | Description                                                     |
|--------------|---------|-----------------------------------------------------------------|
| delete_all   | false   | If true, all of the listed instances are deleted                |
| **name**     |         | The name of the instance to create                              |
| **image**    |         | The name or id of the image to use                              |
| flavor       | medium  | The flavor to use for the instance                              |
| **key**      |         | The Openstack key to use                                        |
| **ssh_user** |         | The name of the user to use when establishing an ssh connection |
| vol_size     | 16      | The size in GB of the newly created volume for the instance     |

*Note: All bolded values are required*

## Usage

To run the playbook, simply run:

```bash
ansible-playbook playbook.yml
```

After the instances have been provisioned, connectivity can be tested by running:

```bash
ansible-playbook playbook.yml --tags test
```