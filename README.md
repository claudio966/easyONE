# easyONE

## Open Nebula Installation
Para essa instalação, o sistema operacional a ser utilizado é Ubuntu Server 20.04.4; e a versão do OpenNebula é a 6.4:
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





