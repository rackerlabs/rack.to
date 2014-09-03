# Production Setup

Before you begin, you'll need to collect the following (ask @ycombinator):

 * `~/.ssh/drg.pem`
 * The `ansible-vault` password.

1. Download and install [Ansible](http://docs.ansible.com/intro_installation.html#installing-the-control-machine).
   * On Mac OSX machines with [Homebrew](http://brew.sh/) installed, you can simply run: `$ brew install ansible`


2. Install pyrax.

  ```bash
  $ sudo pip install pyrax
  ```

3. Create a file named `~/.rackspace_cloud_credentials` with the following contents:

  ```
  [rackspace_cloud]
  username = <REPLACE WITH YOUR RACKSPACE CLOUD USERNAME>
  api_key = <REPLACE WITH YOUR RACKSPACE CLOUD API KEY>
  ```

4. Make sure the `drg.pem` file is in your `~/.ssh` directory. The corresponding public key needs to be uploaded as the `drg` public key in the "SSH Keys" section of your Rackspace Cloud Control Panel for the region(s) where you wish to setup production infrastructure. Modify file permissions:

  ```bash
  $ chmod 600 ~/.ssh/drg.pem
  ```

5. Change to this directory on your development machine.

  ```bash
  $ cd /path/to/rack.to
  ```

6. Run the Ansible playbook to set up the production environment within a region.

  ```bash
  $ RAX_REGION=DFW ansible-playbook --ask-vault-pass -i inventory/ site.yml
  ```
