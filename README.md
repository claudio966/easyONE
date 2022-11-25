# easyONE

## Open Nebula Installation
For this installation, the operational system used will be Ubuntu Server 20.04.4; The OpenNebula version is 6.4:

- SO: Ubuntu Server 20.04.4

- OpenNebula: 6.4

- Hypervisor: KVM

The hypervisor choice will be understandable later. But, take in mind that choice can be different for your host.

### Importing credentials for ONE repository
```bash
wget -q -O- https://downloads.opennebula.org/repo/repo.key | sudo apt-key add -
```

### Adding ONE repository on the System
```bash
echo "deb https://downloads.opennebula.org/repo/6.4/Ubuntu/20.04 stable opennebula" | sudo tee /etc/apt/sources.list.d/opennebula.list
```

### Installing MariaDB Server
```bash
sudo apt update && sudo apt install mariadb-server -y
```

### Configuring MariaDB Server
```bash
sudo mysql -u root -p 
```

### Creating a New database
Access the mariaDB, with your credentials previously configured, with below command:
```bash
sudo mysql -u root -p
```

### Execute the following DDL's and DCL's
```sql
CREATE DATABASE opennebula;
```

```sql
GRANT ALL PRIVILEGES ON opennebula.* TO 'oneadmin' IDENTIFIED BY 'StrongPassword';
```

```sql
FLUSH PRIVILEGES;
```

```sql
EXIT
```

### Installing ONE dependencies via APT
```bash
sudo apt update && sudo apt install opennebula opennebula-sunstone opennebula-gate opennebula-flow opennebula-fireedge opennebula-provision -y
```

### Installing complementary dependencies via Ruby Gems
```bash
sudo /usr/share/one/install_gems
```

### Configuring ONE Backend
After the installation of ONE dependencies, go and open in, with any text editor(VIM :)). the file `oned.conf` at /etc/one/; like below:
```bash
sudo vim /etc/one/oned.conf
```

Search for a variable called DB, and insert the information like the below model:
```bash
DB = [ BACKEND = "mysql",
      SERVER = "localhost",
      PORT = 0,
      USER = "oneadmin",
      PASSWD = "StrongPassword",
      DB_NAME = "opennebula" ]
```

:information_source: The `passwd` field is the same defined in the oneadmin user configuration of MariaDB server.

### Opening the 9869 Port for OpenNebula Sunstone(Dashboard)
Using `ufw` tool or another one, opening 9869 port used by Sunstone:
```bash
sudo ufw allow proto tcp from any to any port 9869
```

### Installing dependencies for a KVM Node
This installation can be optional, if you want another hypervisor. But, notice, any hypervisor need to be choosen. Below, there is a list with some options to choice:
- LXC
- LXD
- VMware Vcenter
- QEMU
- Firecracker

With KVM:
```bash
sudo apt install opennebula-node
```

### Configuring Fireedge
The fireedge configuration allow in the deploy moment of a VM in the OpenNebula, can be possible visualize the console terminal of your virtual machine in your browser.











