### **Setting up an account**
In order to create your an account on the CHEMBIO cluster please contact Silvio or Bartosz via e-mail.

** After the account is approved you will receive credentials via e-mail from the <code> it @ cent.uw.edu.pl </code> address.**

The obtained password will allow you to login to the entry node (jumphost-59) at <code>sih-59.cent.uw.edu.pl</code> and from there 
to login to the CHEMBIO cluster front-node (ssh CHEMBIO) and use the compute [nodes](resources.md) <code>ogr-[0-1] and troll-[1]</code>.

** Please familiarize yourself with the general rules of cluster usage before proceeding
further - [LINK](rules.md) **

!!! Warning
    **Important:** in case of lost password or other technical difficulties related to the **entry node** 
    (not cluster front node or compute nodes) please reach out to the IT department at CeNT UW - address: <code>it @ cent.uw.edu.pl</code>.
    
    Include the <code>[sih-59]</code> prefix in the message title and add cluster administrators @Maciek and @Pawel in CC.

!!! Information
    **Please note that password changes on each of the compute nodes and the entry node are synced. It is advised to change your initially obtained password after first login.**

### **Connecting via SSH**
Connections to the CHEMBIO cluster are handled via SSH protocol. See the figure below
for a brief introduction of the network organization:
![Screenshot](img/CHEMBIO_scheme.png)

In order to login to the entry node you can issue the following command:

```sh
ssh your_username@sih-59.cent.uw.edu.pl
```
This will bring you to the **entry node (jumphost-59)**, afterwards you can connect to the CHEMBIO (10.10.59.30) front node and submit tasks to the **compute nodes** 
([click here](resources.md) for a complete list of available resources), for example:
```sh
ssh your_username@10.10.59.30
```

**In order to simplify file copying and every day work the suggested way of connecting
to the <code>CHEMBIO</code>cluster is to use [sshuttle](https://github.com/sshuttle/sshuttle). This allows to
bypass the login node and work almost the same way as being connected via VPN to the local network.**

!!! Example
    Assuming <code>sshuttle</code> was installed according to the [guide](https://sshuttle.readthedocs.io/en/stable/installation.html)
    you can connect as follows:
    ```sh
    sshuttle --dns -NHr your_username@sih-59.cent.uw.edu.pl 10.10.59.1/24
    ```
    Once connection is established you can directly login to the CHEMBIO front node or compute nodes using:
    ```sh
    ssh your_username@CHEMBIO.sih-59.internal
    ```
    
!!! Information
    Additionally, depending on your computer and network settings, you may have to connect to <code>CHEMBIO</code> nodes 
    once without <code>sshuttle</code> so that SSH connections are properly configured.

To avoid putting password during each login you can set up authorization via a certificate - additional information
is available [here](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)

### **Work environment**
Each user has access a personal directory and can use the shared workspace:

- <code>/home/users/your_username</code>
- <code>/workspace</code>
!!! Warning
    **These folders are shared between all nodes of the CHEMBIO cluster as well as the jumphost-59.** 

[//]: # (    &#40;please follow the [guidelines]&#40;faq.md#what-are-the-guidelines-for-homenfs-distributed-filesystem-use&#41;&#41;.)

### **Transferring files**
The recommended options to send or fetch files from CHEMBIO cluster are either <code>scp</code> or <code>rsync</code>.

### **Next steps**
Once the basics are set up you should be able to start running calculations. Follow the next chapter for more details.
