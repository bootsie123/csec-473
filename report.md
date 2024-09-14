John Arrandale\
jca7237@rit.edu\
Echo\
2241 Fall

For installation instructions and requirements as well as usage info, see the `README.md` file.

### What is the goal of these Ansible scripts? What purpose does it bring to the Gray team effort (or possibly Red or Blue)?

This Ansible playbook aims to make provisioning multiple instances to Openstack a breeze. By specifing a list of instances to create in `vars.yml`, a user can automatically provision or delete the specified instances. An Ansible inventory file (`inventory.ini`) will automatically be created and any ssh keys added to the `files/keys` directory will also automatically be uploaded to Openstack.

This playbook can also be directly imported by other playbooks or used as a starting point when deploying and configuring services. Because of this, it brings a great deal of utility to the Gray team effort. When this playbook is combined with others, essentially, the entire competition can be repeatedly and consistently deployed and redeployed.

### What was the most challenging aspect of working with Ansible?

Since I've worked with Ansible before, the basics along with most of the playbook was rather straightforward. However, there is one issue which I encountered that was the most challenging. For some reason, when Ansible tries to SSH into the newly created instances when using the `Connectivity Test` playbook right after the `Provisioning` playbook (ignoring the `never` tag), it will fail to connect and say `Failed to connect to the host via ssh: kex_exchange_identification`. However, it seems this only happens when trying to connect the first time. Any run of the `Connectivity Test` playbook afterwards usually works without any issues.

### If you were to expand this Ansible script, what would you add?

If I was expanding this Ansible playbook further, I'd probably add more instance configuration options. This might be options such as specifying a list of networks, a list of security groups, or even being able to add a custimization script which runs on first boot. Other additions would be more ease-of-use related such as checking if an instance already exists before creating it or creating a way to convert an instance into an image.