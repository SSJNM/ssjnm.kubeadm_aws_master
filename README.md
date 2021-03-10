Role - Kubeadm AWS Master
=========

The role intends to configure Kubernetes Master launched in AWS cloud

Requirements
------------

- Needs python-3.6+ with *boto* library installed in your system
- Make sure ssh_pass software is installed and host_key_check should be false in config file other wise we need to verify fingerprint 

Role Variables
--------------
There are some necessary variable that needs to be defined before using this role
Other variable that may be changed in future are also attached with (*defaults/main.yml*)

**Necessary variables:**

- files_path: Here we have to pass the folder location/directory where we have put token-master file which contains the join command for Kube-slave 
- Example --> files_path: /root/kubeadm_cloud/files/

Note:- The final path of files folder should be mentioned with / sign for directory. 

**Default variables:** These variables are not neccesary to be passed and will accept default values when nothing passed in var_file

- pod_cidr: Default pod cidr that we want But changing this might lead to Core-DNS failure
- Ex --> pod_cidr: 10.240.0.0/16

By default we are using flannel as cni layer so Mention the command

- cni_layer_command: Command for particular CNI plugin to be attached
- Ex --> cni_layer_command: "kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml"

Dependencies
------------

None

Example Playbook
----------------

Configuring the KubeMaster with pod_cidr to be 10.240.0.0/16 and passing the flannel cni command
With working directory to be /root/kubeadm_cloud/ and dowloading the token on relative-directory files/ 

    - hosts: KubeMaster
      vars:
        files_path: /root/kubeadm_cloud/files/
        pod_cidr: 10.240.0.0/16
        cni_layer_command: "kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml"
      roles:
         - role: ssjnm.kubead,_aws_master


Author Information
------------------

This role was created by Nishant Singh, GitHub User - [SSJNM]

[SSJNM]: <https://github.com/SSJNM>