# saltstack-salt-in-10-minutes

# 🚀 Install and configure Saltstack Salt master and minion 🚀

https://github.com/coding-to-music/saltstack-salt-in-10-minutes

From / By https://docs.saltproject.io/en/master/topics/tutorials/walkthrough.html

## Environment variables:

```java

```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/saltstack-salt-in-10-minutes.git
git push -u origin main
```

## Install instructions

https://docs.saltproject.io/salt/install-guide/en/latest/

https://docs.saltproject.io/salt/install-guide/en/latest/topics/bootstrap.html#install-bootstrap

https://github.com/saltstack/salt/blob/master/doc/topics/tutorials/walkthrough.rst

.. \_tutorial-salt-walk-through:

# Salt in 10 Minutes

```
Welcome to Salt Project! I am excited that you are interested in Salt and
starting down the path to better infrastructure management. I developed
(and am continuing to develop) Salt with the goal of making the best
software available to manage computers of almost any kind. I hope you enjoy
working with Salt and that the software can solve your real world needs!

    - Thomas S Hatch
    - Salt Project creator and Chief Developer of Salt Project
```

# Getting Started

## What is Salt?

Salt is a different approach to infrastructure management, founded on
the idea that high-speed communication with large numbers of systems can open
up new capabilities. This approach makes Salt a powerful multitasking system
that can solve many specific problems in an infrastructure.

The backbone of Salt is the remote execution engine, which creates a high-speed,
secure and bi-directional communication net for groups of systems. On top of this
communication system, Salt provides an extremely fast, flexible, and easy-to-use
configuration management system called `Salt States`.

## Installing Salt

SaltStack has been made to be very easy to install and get started. The
`Salt install guide <https://docs.saltproject.io/salt/install-guide/en/latest/>`\_
provides instructions for all supported platforms.

IMPORTANT ANNOUNCEMENT:

- repo.saltproject.io has migrated to packages.broadcom.com!
- Click here for latest update (2024-11-22)
- https://saltproject.io/blog/post-migration-salt-project-faqs/

This URL no longer works:

https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/ubuntu.html

This URL works:

https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html

```bash
sudo apt-get update
```

### Add the SaltStack Repository

First, add the SaltStack repository to your system:

```bash
# this did not work
sudo add-apt-repository ppa:saltstack/salt
```

Output

```java
sudo add-apt-repository ppa:saltstack/salt

Repository: 'Types: deb
URIs: https://ppa.launchpadcontent.net/saltstack/salt/ubuntu/
Suites: noble
Components: main
'
Description:
Salt, the remote execution and configuration management tool.
More info: https://launchpad.net/~saltstack/+archive/ubuntu/salt
Adding repository.
Press [ENTER] to continue or Ctrl-c to cancel.
Hit:1 http://security.ubuntu.com/ubuntu noble-security InRelease
Hit:2 http://archive.ubuntu.com/ubuntu noble InRelease
Hit:3 http://archive.ubuntu.com/ubuntu noble-updates InRelease
Hit:4 http://archive.ubuntu.com/ubuntu noble-backports InRelease
Ign:5 https://ppa.launchpadcontent.net/saltstack/salt/ubuntu noble InRelease
Err:6 https://ppa.launchpadcontent.net/saltstack/salt/ubuntu noble Release
  404  Not Found [IP: 2620:2d:4000:1::81 443]
Reading package lists... Done
E: The repository 'https://ppa.launchpadcontent.net/saltstack/salt/ubuntu noble Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```

Needed to remove the launchpad stuff via:

```java
sudo add-apt-repository --remove ppa:saltstack/salt
```

## Install Salt DEBs

https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html

1. Run the following command to install the Salt Project repository:

```java
# Ensure keyrings dir exists

mkdir -p /etc/apt/keyrings

# Download public key

curl -fsSL https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public | sudo tee /etc/apt/keyrings/salt-archive-keyring.pgp

# Create apt repo target configuration

curl -fsSL https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources | sudo tee /etc/apt/sources.list.d/salt.sources
```

2. Run `sudo apt update` to update metadata.

```java
sudo apt update
```

3. Install the salt-minion, salt-master, or other Salt components:

### 3006 LTS

Populate `/etc/apt/preferences.d/salt-pin-1001` in order to restrict upgrades to Salt `3006.x LTS`:

```java
echo 'Package: salt-*
Pin: version 3006.*
Pin-Priority: 1001' | sudo tee /etc/apt/preferences.d/salt-pin-1001
```

Available installs:

```java
sudo apt-get install salt-master
sudo apt-get install salt-minion
sudo apt-get install salt-ssh
sudo apt-get install salt-syndic
sudo apt-get install salt-cloud
sudo apt-get install salt-api
```

### How do I check the version of Ubuntu I am running

http://askubuntu.com/questions/686239/ddg#686249

As said in the official page, use:

```bash
lsb_release -a
```

```bash
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.6 LTS
Release:        20.04
Codename:       focal
```

Your version appears on the "Description" line.

https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/ubuntu.html#install-salt-on-ubuntu-20-04-focal-amd64

To pin your Salt upgrades to the Latest Onedir package of Salt for Ubuntu 20.04 (Focal):

```bash
mkdir /etc/apt/keyrings
```

```bash
sudo curl -fsSL -o /etc/apt/keyrings/salt-archive-keyring-2023.gpg https://repo.saltproject.io/salt/py3/ubuntu/20.04/amd64/SALT-PROJECT-GPG-PUBKEY-2023.gpg

echo "deb [signed-by=/etc/apt/keyrings/salt-archive-keyring-2023.gpg arch=amd64] https://repo.saltproject.io/salt/py3/ubuntu/20.04/amd64/latest focal main" | sudo tee /etc/apt/sources.list.d/salt.list
```

Run `sudo apt-get update` to update your packages.

Install the salt-minion, salt-master, or other Salt components:

```bash
sudo apt-get install salt-master
sudo apt-get install salt-minion
sudo apt-get install salt-ssh
sudo apt-get install salt-syndic
sudo apt-get install salt-cloud
sudo apt-get install salt-api
```

Enable and start the services for salt-minion, salt-master, or other Salt components:

```bash
sudo systemctl enable salt-master && sudo systemctl start salt-master
sudo systemctl enable salt-minion && sudo systemctl start salt-minion
sudo systemctl enable salt-syndic && sudo systemctl start salt-syndic
sudo systemctl enable salt-api && sudo systemctl start salt-api
```

May need to do this to set the ownership and permissions

```java
sudo chown -R salt:salt /var/run/salt
sudo chmod -R 755 /var/run/salt

sudo chown -R salt:salt /etc/salt/pki/minion
sudo chmod -R 755 /etc/salt/pki/minion

sudo chown -R salt:salt /var/cache/salt/minion
sudo chmod -R 755 /var/cache/salt/minion

sudo mkdir -p /var/cache/salt/minion/proc
sudo chown -R salt:salt /var/cache/salt/minion/proc
sudo chmod -R 755 /var/cache/salt/minion/proc

sudo chown -R salt:salt /var/log/salt
sudo chmod -R 755 /var/log/salt

sudo chown -R salt:salt /var/cache/salt/minion
sudo chmod -R 755 /var/cache/salt/minion
sudo mkdir -p /var/cache/salt/minion/schedule
sudo chown -R salt:salt /var/cache/salt/minion/schedule
sudo chmod -R 755 /var/cache/salt/minion/schedule

sudo usermod -aG root salt
```

May need to ensure content of: `/etc/tmpfiles.d/salt.conf`

```java
echo "d /var/run/salt 0755 salt salt -" | sudo tee /etc/tmpfiles.d/salt.conf
```

May need to ensure content of: `/etc/systemd/system/salt-minion.service.d/override.conf`

sudo cat /etc/systemd/system/salt-minion.service.d/override.conf

Should look like this:

```java
[Service]
User=salt
Group=salt
```

Manually create the PID file with the correct permissions:

```java
sudo touch /var/run/process_responsibility_salt-minion.pid
sudo chown salt:salt /var/run/process_responsibility_salt-minion.pid
sudo chmod 644 /var/run/process_responsibility_salt-minion.pid
```

Manually restart both the salt master and minion

```java
sudo systemctl restart salt-master
sudo systemctl restart salt-minion
```

Check the status of the salt master and minion

```java
sudo systemctl status salt-master
sudo systemctl status salt-minion
```

Check the logs on the Salt Master

```java
sudo journalctl -u salt-master
```

Check the logs on the Salt Minions

```java
sudo journalctl -u salt-minion
```

#### Check the status of what is running

```java
docker ps

sudo systemctl status

sudo systemctl status salt-master salt-minion salt-syndic salt-api

sudo systemctl status salt-minion

sudo systemctl list-units

sudo systemctl list-units --state=degraded

sudo systemctl list-units --state=failed
```

Note

When you install a onedir version of Salt (3006 and later), Salt installs its own local version of Python and the dependencies needed for the core functionality of Salt.

After installing a onedir verison of Salt, your system has both a global version of Python at the system level and a local version of Python used by Salt. This architecture change means that the Salt onedir paths for Python are different and you need to change how you install third-party Python dependencies that you use with Salt, including your state files. See Install dependencies for more information.

### ensure that ports 4505 and 4506 are open on all servers where the Salt Minions are running. These ports are used for communication between the Salt Master and the Minions:

- Port 4505: Used for the publish/subscribe system, allowing the Master to send commands to the Minions.

- Port 4506: Used for the return system, allowing Minions to send responses back to the Master.

Here’s how you can open these ports using ufw (Uncomplicated Firewall) on Ubuntu:

Open Ports on the Minions:

```bash
sudo ufw allow 4505/tcp
sudo ufw allow 4506/tcp
sudo ufw reload
```

Open Ports on the Master (if you have a firewall running on the Master):

```bash
sudo ufw allow 4505/tcp
sudo ufw allow 4506/tcp
sudo ufw reload
```

### To ensure that the UFW (Uncomplicated Firewall) is always running on your Ubuntu system, you can follow these steps:

Enable UFW:

```bash
sudo ufw enable
```

Check UFW Status:

```bash
sudo ufw status
```

This command will show you the current status of UFW. If it is active, it will display “Status: active”.

Enable UFW to Start on Boot: UFW should automatically start on boot once it is enabled. However, you can verify this by checking the UFW service status:

```bash
sudo systemctl status ufw
```

If it is not enabled, you can enable it with:

```bash
sudo systemctl enable ufw
```

## Allow SSH through UFW:

Open a terminal on the server.

Run the following command to allow SSH connections:

```bash
sudo ufw allow ssh
```

Alternatively, you can specify the port number directly:

```bash
sudo ufw allow 22/tcp
```

Verify UFW status:

Check the status of UFW to ensure the rule has been applied:

```bash
sudo ufw status
```

You should see a line indicating that port 22 (SSH) is allowed.

Reload UFW (if necessary):

If the changes don’t take effect immediately, you can reload UFW:

```bash
sudo ufw reload
```

#### Configure Default Policies: It’s a good practice to set default policies to deny all incoming connections and allow all outgoing connections:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

### Check the minions can talk with the master

```bash
nc -v -z <master-ip> 4505
nc -v -z <master-ip> 4506
```

Check UFW Rules: Ensure that the necessary ports (4505 and 4506) are open on the master:

```bash
sudo ufw allow 4505
sudo ufw allow 4506
```

Verify Network Connectivity: Make sure that the minions can reach the master IP address. You can use ping to test basic connectivity:

```bash
ping <master-ip>
```

Check Salt Master Configuration: Ensure that the Salt master is configured to listen on the correct IP address. In the master configuration file (/etc/salt/master), check the interface setting:

```bash
sudo vi /etc/salt/master
```

```bash
interface: 0.0.0.0
```

This setting allows the master to listen on all available network interfaces.

Restart Salt Services: After making any changes, restart the Salt master and minion services:

```bash
sudo systemctl restart salt-master
sudo systemctl restart salt-minion
```

```bash
sudo systemctl status salt-master
sudo systemctl status salt-minion
```

Check Logs for Errors: Look at the logs on both the master and minion for any error messages that might provide more insight:

```bash
sudo tail -n 50 -f /var/log/salt/master
sudo tail -n 50 -f /var/log/salt/minion
```

Firewall on Minions: If the minions have their own firewalls, ensure that they allow outgoing connections to ports 4505 and 4506:

```bash
sudo ufw allow out to <master-ip> port 4505
sudo ufw allow out to <master-ip> port 4506
```

#### Check Permissions:

Ensure that the Salt Minion has the necessary permissions to write to the log file and create directories. You can adjust the permissions using the following commands:

```bash
sudo chown -R salt:salt /var/log/salt
sudo chown -R salt:salt /etc/salt/pki
```

#### Verify Configuration:

Make sure the configuration files are correctly set up and that there are no syntax errors. You can check the configuration with:

```bash
sudo salt-minion --config-dir=/etc/salt -l debug
```

#### Run in Foreground:

Running the Salt Minion in the foreground can provide more detailed error messages:

```bash
sudo salt-minion -l debug
```

It seems like the Salt Minion is having trouble authenticating with the Salt Master due to a cached public key issue. Here are some steps to resolve this:

#### Clear Cached Keys:

On the Salt Master, delete the cached public key for the minion:

```bash
sudo salt-key -d <minion_id>
```

#### Verify that the key has been deleted:

```bash
sudo salt-key -L
```

#### Restart the Minion:

On the Minion, restart the Salt Minion service to generate a new key pair:

```bash
sudo systemctl restart salt-minion
```

#### Accept the New Key:

On the Salt Master, accept the new key from the minion:

```bash
sudo salt-key -A
```

#### Check Firewall Settings:

Ensure that the necessary ports (4505 and 4506) are open on both the master and minion. You can check port connectivity using nc:

```bash
nc -v -z <master_ip> 4505
nc -v -z <master_ip> 4506
```

#### Verify Configuration:

Ensure that the master and minion configurations are correct. The minion configuration file (/etc/salt/minion) should have the correct master IP address:

```bash
master: <master_ip>
```

#### Run in Debug Mode:

Running the minion in debug mode can provide more detailed error messages:

```bash
sudo salt-minion -l debug
```

## configure the Salt minion to connect to the same machine where the Salt master is running

To configure the Salt minion to connect to the same machine where the Salt master is running, you can set the master value to `localhost` or `127.0.0.1` in the minion configuration file. Here’s how you can do it:

Open the Minion Configuration File:

```bash
sudo nano /etc/salt/minion
```

Set the Master Value: Find the line that starts with #master: and update it to point to localhost or 127.0.0.1:

```bash
master: localhost
```

Save and Exit: Save the changes and exit the editor (in Nano, you can do this by pressing Ctrl+O to save and Ctrl+X to exit).
Here’s an example of what the relevant part of your /etc/salt/minion file might look like:

# Set the master address

```bash
master: localhost
```

Restart the Minion Service: After making these changes, restart the minion service to apply the new configuration:

```bash
sudo systemctl restart salt-minion
```

Check the Status: Verify that the minion is running and connected to the master:

```bash
sudo systemctl status salt-minion
```

List and Accept the Minion Key: Check if the minion key appears under “Unaccepted Keys” and accept it:

```bash
sudo salt-key -L
sudo salt-key -A
```

This setup ensures that the minion connects to the master running on the same machine

#### should I edit /etc/salt/minion or instead minion.d/\*.conf ?

You can use either approach, but it’s generally recommended to use the minion.d/\*.conf directory for custom configurations. This way, you can keep your configurations modular and organized. Here’s how you can proceed:

Create a new configuration file in the `/etc/salt/minion.d/` directory, for example, `/etc/salt/minion.d/custom.conf`

Add your custom configurations in this file. For instance:

```bash
master: <master_ip_address>
```

After installing Salt on your operating system, you need to complete the following post-installation steps:

- Configure the Salt master and minions https://docs.saltproject.io/salt/install-guide/en/latest/topics/configure-master-minion.html#configure-master-minion

View the full 1300 line default conf file `/etc/salt/master` with almost everything commented out

more `code /etc/salt/master`

Instead put a minimal conf file into `/etc/salt/master.d/network.conf`

sudo vi `/etc/salt/master.d/network.conf`

Find your ip address

```bash
hostname -i
```

Example Output

```bash
192.168.1.10 10.0.0.5
```

In this example, if `192.168.1.10` is your primary IP address, you would use that in your `/etc/salt/master.d/network.conf` file.

If you’re unsure which IP address to use, you can check your network interfaces with:

```bash
ip addr
```

Alternatively, you can use SaltStack itself to get the hostname by running:

```bash
salt '*' network.get_hostname
```

If you need to set or modify the hostname, you can use:

```bash
salt '*' network.mod_hostname <new_hostname>
```

```bash
# The network interface to bind to
interface: 192.0.2.20 -- example address

# The Request/Reply port
ret_port: 4506

# The port minions bind to for commands, aka the publish port
publish_port: 4505
```

This will show you if the Salt master is listening on port 4505 (the default port for Salt master).

### Once you’ve set the value in your /etc/salt/master.d/network.conf file, you’ll need to restart the Salt master service to apply the changes. You can do this with the following command:

```bash
sudo systemctl restart salt-master
```

and

```bash
sudo systemctl restart salt-minion
```

After restarting, you can check the status of the Salt master to ensure it’s running correctly:

```bash
sudo systemctl status salt-master
```

and

```bash
sudo systemctl status salt-minion
```

or

```bash
sudo service salt-master status
```

### Check Network Connectivity: Ensure that the Minions can reach the Master on the required ports (4505 and 4506). You can test this using nc (netcat):

```bash
nc -v -z <master-ip> 4505
nc -v -z <master-ip> 4506
```

### To validate that your Salt master is correctly using the new configuration, you can follow these steps:

1. Check the Salt Master Logs: Look at the Salt master logs to see if there are any errors or warnings related to the network configuration. You can view the logs with:

```bash
sudo journalctl -u salt-master -f
```

2. Verify the Listening IP Address: Ensure that the Salt master is listening on the correct IP address. You can use the netstat or ss command to check this:

```bash
sudo netstat -tuln | grep 4505
```

or

```bash
sudo ss -tuln | grep 4505
```

3. Test Communication with a Minion: Try to ping a Salt minion from the master to ensure communication is working:

```bash
sudo salt '*' test.ping
```

If the minions respond with True, it means they can communicate with the master.

4. Check the Master Configuration: You can also check the effective configuration of the Salt master to ensure your changes are applied. Run:

```bash
sudo salt-master --versions-report
```

This will show you the current configuration and versions of the Salt master.

## more

- Start the master and minion services https://docs.saltproject.io/salt/install-guide/en/latest/topics/start-salt-services.html#start-salt-services

- Accept the minion keys https://docs.saltproject.io/salt/install-guide/en/latest/topics/accept-keys.html#accept-keys

- Verify a Salt install https://docs.saltproject.io/salt/install-guide/en/latest/topics/verify-install.html#verify-install

- Install dependencies https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-dependencies.html#install-dependencies

## Starting Salt

Salt functions on a master/minion topology. A master server acts as a
central control bus for the clients, which are called `minions`. The minions
connect back to the master.

### Setting Up the Salt Master

Turning on the Salt Master is easy -- just turn it on! The default configuration
is suitable for the vast majority of installations. The Salt Master can be
controlled by the local Linux/Unix service manager:

On Systemd based platforms (newer Debian, openSUSE, Fedora):

```bash
    systemctl start salt-master
```

On Upstart based systems (Ubuntu, older Fedora/RHEL):

```bash
    service salt-master start
```

On SysV Init systems (Gentoo, older Debian etc.):

```bash
    /etc/init.d/salt-master start
```

Alternatively, the Master can be started directly on the command-line:

```bash
    salt-master -d
```

The Salt Master can also be started in the foreground in debug mode, thus
greatly increasing the command output:

```bash
    salt-master -l debug
```

The Salt Master needs to bind to two TCP network ports on the system. These ports
are `4505` and `4506`. For more in depth information on firewalling these ports,
the firewall tutorial is available :ref:`here <firewall>`.

.. \_master-dns:

### Finding the Salt Master

When a minion starts, by default it searches for a system that resolves to the `salt` hostname on the network.
If found, the minion initiates the handshake and key authentication process with the Salt master.
This means that the easiest configuration approach is to set internal DNS to resolve the name `salt` back to the Salt Master IP.

Otherwise, the minion configuration file will need to be edited so that the
configuration option `master` points to the DNS name or the IP of the Salt Master:

```

    The default location of the configuration files is ``/etc/salt``. Most
    platforms adhere to this convention, but platforms such as FreeBSD and
    Microsoft Windows place this file in different locations.
```

`/etc/salt/minion:`

```yaml
master: saltmaster.example.com
```

### Setting up a Salt Minion

```

    The Salt Minion can operate with or without a Salt Master. This walk-through
    assumes that the minion will be connected to the master, for information on
    how to run a master-less minion please see the master-less quick-start guide:
```

    :ref:`Masterless Minion Quickstart <masterless-quickstart>`

Now that the master can be found, start the minion in the same way as the
master; with the platform init system or via the command line directly:

As a daemon:

```bash
    salt-minion -d
```

In the foreground in debug mode:

```bash
    salt-minion -l debug
```

.. \_minion-id-generation:

When the minion is started, it will generate an `id` value, unless it has
been generated on a previous run and cached (in `/etc/salt/minion_id` by
default). This is the name by which the minion will attempt
to authenticate to the master. The following steps are attempted, in order to
try to find a value that is not `localhost`:

1. The Python function `socket.getfqdn()` is run
2. `/etc/hostname` is checked (non-Windows only)
3. `/etc/hosts` (`%WINDIR%\system32\drivers\etc\hosts` on Windows hosts) is
   checked for hostnames that map to anything within :strong:`127.0.0.0/8`.

If none of the above are able to produce an id which is not `localhost`, then
a sorted list of IP addresses on the minion (excluding any within
:strong:`127.0.0.0/8`) is inspected. The first publicly-routable IP address is
used, if there is one. Otherwise, the first privately-routable IP address is
used.

If all else fails, then `localhost` is used as a fallback.

```Overriding the`id`

    The minion id can be manually specified using the :conf_minion:`id`
    parameter in the minion config file.  If this configuration value is
    specified, it will override all other sources for the ``id``.

Now that the minion is started, it will generate cryptographic keys and attempt
to connect to the master. The next step is to venture back to the master server
and accept the new minion's public key.

.. \_using-salt-key:

### Using salt-key

Salt authenticates minions using public-key encryption and authentication. For
a minion to start accepting commands from the master, the minion keys need to be
accepted by the master.

The `salt-key` command is used to manage all of the keys on the
master. To list the keys that are on the master:

```bash
    salt-key -L
```

The keys that have been rejected, accepted, and pending acceptance are listed.
The easiest way to accept the minion key is to accept all pending keys:

```bash
    salt-key -A
```

```

    Keys should be verified! Print the master key fingerprint by running ``salt-key -F master``
    on the Salt master. Copy the ``master.pub`` fingerprint from the Local Keys section,
    and then set this value as the :conf_minion:`master_finger` in the minion configuration
    file. Restart the Salt minion.

    On the master, run ``salt-key -f minion-id`` to print the fingerprint of the
    minion's public key that was received by the master. On the minion, run
    ``salt-call key.finger --local`` to print the fingerprint of the minion key.
```

    On the master:

```bash
        # salt-key -f foo.domain.com
        Unaccepted Keys:
        foo.domain.com:  39:f9:e4:8a:aa:74:8d:52:1a:ec:92:03:82:09:c8:f9
```

    On the minion:

```bash
        # salt-call key.finger --local
        local:
            39:f9:e4:8a:aa:74:8d:52:1a:ec:92:03:82:09:c8:f9
```

    If they match, approve the key with ``salt-key -a foo.domain.com``.

### Sending the First Commands

Now that the minion is connected to the master and authenticated, the master
can start to command the minion.

Salt commands allow for a vast set of functions to be executed and for
specific minions and groups of minions to be targeted for execution.

The `salt` command is comprised of command options, target specification,
the function to execute, and arguments to the function.

A simple command to
start with looks like this:

```bash
    salt '*' test.version
```

The `*` is the target, which specifies all minions.

`test.version` tells the minion to run the :py:func:`test.version
<salt.modules.test.version>` function.

In the case of `test.version`, `test` refers to a :ref:`execution module
<writing-execution-modules>`. `version` refers to the :py:func:`version
<salt.modules.test.version>` function contained in the aforementioned `test`
module.

```

    Execution modules are the workhorses of Salt. They do the work on the
    system to perform various tasks, such as manipulating files and restarting
    services.

The result of running this command will be the master instructing all of the
minions to execute :py:func:`test.version <salt.modules.test.version>` in parallel
and return the result. Using :py:func:`test.version <salt.modules.test.version>`
is a good way of confirming that a minion is connected, and reaffirm to the user
the salt version(s) they have installed on the minions.

```

    Each minion registers itself with a unique minion ID. This ID defaults to
    the minion's hostname, but can be explicitly defined in the minion config as
    well by using the :conf_minion:`id` parameter.

Of course, there are hundreds of other modules that can be called just as
`test.version` can. For example, the following would return disk usage on all
targeted minions:

```bash
    salt '*' disk.usage
```

### Getting to Know the Functions

Salt comes with a vast library of functions available for execution, and Salt
functions are self-documenting. To see what functions are available on the
minions execute the :py:func:`sys.doc <salt.modules.sys.doc>` function:

```bash
    salt '*' sys.doc
```

This will display a very large list of available functions and documentation on
them.

```
Module documentation is also available :ref:`on the web <all-salt.modules>`.

These functions cover everything from shelling out to package management to
manipulating database servers. They comprise a powerful system management API
which is the backbone to Salt configuration management and many other aspects
of Salt.

```

    Salt comes with many plugin systems. The functions that are available via
    the ``salt`` command are called :ref:`Execution Modules <all-salt.modules>`.

### Helpful Functions to Know

The :mod:`cmd <salt.modules.cmdmod>` module contains
functions to shell out on minions, such as :mod:`cmd.run
<salt.modules.cmdmod.run>` and :mod:`cmd.run_all
<salt.modules.cmdmod.run_all>`:

```bash
    salt '*' cmd.run 'ls -l /etc'
```

The `pkg` functions automatically map local system package managers to the
same salt functions. This means that `pkg.install` will install packages via
`yum` on Red Hat based systems, `apt` on Debian systems, etc.:

```bash
    salt '*' pkg.install vim
```

```
Some custom Linux spins and derivatives of other distributions are not properly
detected by Salt. If the above command returns an error message saying that
`pkg.install` is not available, then you may need to override the pkg
provider. This process is explained :ref:`here <state-providers>`.

The :mod:`network.interfaces <salt.modules.network.interfaces>` function will
list all interfaces on a minion, along with their IP addresses, netmasks, MAC
addresses, etc:
```

```bash
    salt '*' network.interfaces
```

### Changing the Output Format

The default output format used for most Salt commands is called the `nested`
outputter, but there are several other outputters that can be used to change
the way the output is displayed. For instance, the `pprint` outputter can be
used to display the return data using Python's `pprint` module:

```bash
    root@saltmaster:~# salt myminion grains.item pythonpath --out=pprint
    {'myminion': {'pythonpath': ['/usr/lib64/python2.7',
                                 '/usr/lib/python2.7/plat-linux2',
                                 '/usr/lib64/python2.7/lib-tk',
                                 '/usr/lib/python2.7/lib-tk',
                                 '/usr/lib/python2.7/site-packages',
                                 '/usr/lib/python2.7/site-packages/gst-0.10',
                                 '/usr/lib/python2.7/site-packages/gtk-2.0']}}
```

The full list of Salt outputters, as well as example output, can be found
:ref:`here <all-salt.output>`.

### salt-call

The examples so far have described running commands from the Master using the
`salt` command, but when troubleshooting it can be more beneficial to login
to the minion directly and use `salt-call`.

Doing so allows you to see the minion log messages specific to the command you
are running (which are _not_ part of the return data you see when running the
command from the Master using `salt`), making it unnecessary to tail the
minion log. More information on `salt-call` and how to use it can be found
:ref:`here <using-salt-call>`.

#### Grains

Salt uses a system called :ref:`Grains <targeting-grains>` to build up
static data about minions. This data includes information about the operating
system that is running, CPU architecture and much more. The grains system is
used throughout Salt to deliver platform data to many components and to users.

Grains can also be statically set, this makes it easy to assign values to
minions for grouping and managing.

A common practice is to assign grains to minions to specify what the role or
roles a minion might be. These static grains can be set in the minion
configuration file or via the :mod:`grains.setval <salt.modules.grains.setval>`
function.

#### Targeting

Salt allows for minions to be targeted based on a wide range of criteria. The
default targeting system uses globular expressions to match minions, hence if
there are minions named `larry1`, `larry2`, `curly1`, and `curly2`, a
glob of `larry*` will match `larry1` and `larry2`, and a glob of `*1`
will match `larry1` and `curly1`.

Many other targeting systems can be used other than globs, these systems
include:

#### Regular Expressions

Target using PCRE-compliant regular expressions

#### Grains

Target based on grains data:
:ref:`Targeting with Grains <targeting-grains>`

#### Pillar

Target based on pillar data:
:ref:`Targeting with Pillar <targeting-pillar>`

#### IP

Target based on IP address/subnet/range

#### Compound

Create logic to target based on multiple targets:
:ref:`Targeting with Compound <targeting-compound>`

#### Nodegroup

Target with nodegroups:
:ref:`Targeting with Nodegroup <targeting-nodegroups>`

The concepts of targets are used on the command line with Salt, but also
function in many other areas as well, including the state system and the
systems used for ACLs and user permissions.

### Passing in Arguments

Many of the functions available accept arguments which can be passed in on
the command line:

```bash
    salt '*' pkg.install vim
```

This example passes the argument `vim` to the pkg.install function. Since
many functions can accept more complex input than just a string, the arguments
are parsed through YAML, allowing for more complex data to be sent on the
command line:

```bash
    salt '*' test.echo 'foo: bar'
```

In this case Salt translates the string 'foo: bar' into the dictionary
"{'foo': 'bar'}"

```
    Any line that contains a newline will not be parsed by YAML.
```

# Salt States

Now that the basics are covered the time has come to evaluate `States`. Salt
`States`, or the `State System` is the component of Salt made for
configuration management.

The state system is already available with a basic Salt setup, no additional
configuration is required. States can be set up immediately.

```
    Before diving into the state system, a brief overview of how states are
    constructed will make many of the concepts clearer. Salt states are based
    on data modeling and build on a low level data structure that is used to
    execute each state function. Then more logical layers are built on top of
    each other.

    The high layers of the state system which this tutorial will
    cover consists of everything that needs to be known to use states, the two
    high layers covered here are the `sls` layer and the highest layer
    `highstate`.

    Understanding the layers of data management in the State System will help with
    understanding states, but they never need to be used. Just as understanding
    how a compiler functions assists when learning a programming language,
    understanding what is going on under the hood of a configuration management
    system will also prove to be a valuable asset.
```

### The First SLS Formula

The state system is built on SLS (SaLt State) formulas. These formulas are built out in
files on Salt's file server. To make a very basic SLS formula open up a file
under /srv/salt named vim.sls. The following state ensures that vim is installed
on a system to which that state has been applied.

`/srv/salt/vim.sls:`

```yaml
vim: pkg.installed
```

Now install vim on the minions by calling the SLS directly:

```bash
    salt '*' state.apply vim
```

This command will invoke the state system and run the `vim` SLS.

Now, to beef up the vim SLS formula, a `vimrc` can be added:

`/srv/salt/vim.sls:`

```yaml
vim:
  pkg.installed: []

/etc/vimrc:
  file.managed:
    - source: salt://vimrc
    - mode: 644
    - user: root
    - group: root
```

Now the desired `vimrc` needs to be copied into the Salt file server to
`/srv/salt/vimrc`. In Salt, everything is a file, so no path redirection needs
to be accounted for. The `vimrc` file is placed right next to the `vim.sls` file.
The same command as above can be executed to all the vim SLS formulas and now
include managing the file.

```

    Salt does not need to be restarted/reloaded or have the master manipulated
    in any way when changing SLS formulas. They are instantly available.
```

### Adding Some Depth

Obviously maintaining SLS formulas right in a single directory at the root of
the file server will not scale out to reasonably sized deployments. This is
why more depth is required. Start by making an nginx formula a better way,
make an nginx subdirectory and add an init.sls file:

`/srv/salt/nginx/init.sls:`

```yaml
nginx:
  pkg.installed: []
  service.running:
    - require:
        - pkg: nginx
```

A few concepts are introduced in this SLS formula.

First is the service statement which ensures that the `nginx` service is running.

Of course, the nginx service can't be started unless the package is installed --
hence the `require` statement which sets up a dependency between the two.

The `require` statement makes sure that the required component is executed before
and that it results in success.

```
    The `require` option belongs to a family of options called `requisites`.
    Requisites are a powerful component of Salt States, for more information
    on how requisites work and what is available see:
    :ref:`Requisites <requisites>`

    Also evaluation ordering is available in Salt as well:
    :ref:`Ordering States<ordering>`
```

This new sls formula has a special name -- `init.sls`. When an SLS formula is
named `init.sls` it inherits the name of the directory path that contains it.
This formula can be referenced via the following command:

```bash
    salt '*' state.apply nginx
```

```
:py:func:`state.apply <salt.modules.state.apply_>` is just another remote
execution function, just like :py:func:`test.version <salt.modules.test.version>`
or :py:func:`disk.usage <salt.modules.disk.usage>`. It simply takes the
name of an SLS file as an argument.

Now that subdirectories can be used, the `vim.sls` formula can be cleaned up.
To make things more flexible, move the `vim.sls` and vimrc into a new subdirectory
called `edit` and change the `vim.sls` file to reflect the change:
```

`/srv/salt/edit/vim.sls:`

```yaml
vim: pkg.installed

/etc/vimrc:
  file.managed:
    - source: salt://edit/vimrc
    - mode: 644
    - user: root
    - group: root
```

Only the source path to the vimrc file has changed. Now the formula is
referenced as `edit.vim` because it resides in the edit subdirectory.
Now the edit subdirectory can contain formulas for emacs, nano, joe or any other
editor that may need to be deployed.

### Next Reading

Two walk-throughs are specifically recommended at this point. First, a deeper
run through States, followed by an explanation of Pillar.

1. :ref:`Starting States <starting-states>`

2. :ref:`Pillar Walkthrough <pillar-walk-through>`

An understanding of Pillar is extremely helpful in using States.

### Getting Deeper Into States

Two more in-depth States tutorials exist, which delve much more deeply into States
functionality.

1. :ref:`How Do I Use Salt States? <starting-states>`, covers much
   more to get off the ground with States.

2. The :ref:`States Tutorial<states-tutorial>` also provides a
   fantastic introduction.

These tutorials include much more in-depth information including templating
SLS formulas etc.

### So Much More!

This concludes the initial Salt walk-through, but there are many more things still
to learn! These documents will cover important core aspects of Salt:

- :ref:`Pillar<pillar>`

- :ref:`Job Management<jobs>`

A few more tutorials are also available:

- :ref:`Remote Execution Tutorial<writing-execution-modules>`

- :ref:`Standalone Minion<tutorial-standalone-minion>`

This still is only scratching the surface, many components such as the reactor
and event systems, extending Salt, modular components and more are not covered
here. For an overview of all Salt features and documentation, look at the
:ref:`Table of Contents<table-of-contents>`.
