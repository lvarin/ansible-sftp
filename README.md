# Ansible sftp

This is still a prototype. It makes some assumptions, like that the user exists.

**NOTE:** This modifies the SSH daemon configuration, so it is possible that the daemon configuration gets "misconfigured" and becomes unusable.

## Quick start

1. Create an inventory with the machine(s) you want to install sftp to. One machine per line, for example:

    ```sh
    $ cat inventory
    machine-sft
    $
    ```

1. Edit `site.yaml` and set `sftp_user` to a suitable user. This user will be only able to handle SFTP/SCP/SSHFS. No interactive connection will be accepted by this user. 

1. Then run Ansible:

    ```sh
    ansible-playbook site.yaml -v -i inventory
    ```
    
## Remote mount

It is possible to mount a remote folder using `SSHFS`. There is only 

1. Make sure you have access to the remote machine using ssh:

    ```sh
    $ ssh tesk@YYY.YYY.YYY.YYY
    Last login: Tue Oct 22 12:11:31 2024 from XXX.XXX.XXX.XXX
    This account is currently not available.
    Connection to YYY.YYY.YYY.YYY closed.
    ```

1. Install sshf:

   ```sh
   $ sudo dnf install fuse-sshfs
   ```

1. Mount the folder:

   ```sh
   $ mkdir mount
   $ sshfs tesk@YYY.YYY.YYY.YYY: ~/mount/
   $ ls -l mount
   total 0
   ```
