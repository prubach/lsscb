### **Remote graphical access to Lab Workstations**

There are 2 options depending on whether you want to graphically connect to an existing session 
open on the workstation or you want to remotely start a new one and connect to it.

#### Existing session ####

In the first case the recommended solution is [NoMachine](https://www.nomachine.com/).

Ask the administrator to install it on your workstation if you don't have the necessary privileges.

After the installation the daemon is by default available at port 4000. You'll have to connect to SIH-59
using VPN (ask CeNT IT for an account) or use the [sshuttle](first_steps.md)

#### New remote session ####

The second solution allows creating an independent GUI session. This uses TigerVNC which should be already installed:

!!!First-time Configuration
    1. Set password: ``vncpasswd``
    2. Run for the first time: ``vncserver``
    3. Kill the session: ``vncserver -kill :*``
    4. Replace the contents of the ``$HOME/.vnc/xstartup`` file with:

    ```sh
    #!/bin/sh
    [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
    [ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
    vncconfig -iconic &
    dbus-launch --exit-with-session gnome-session
    ```
!!! Starting-stopping

    1. Start a new session adjusting the color depth and screen size:
    ``sh
    vncserver -localhost no -geometry 1800x900 -depth 24``
    2. To kill your session use: ``vncserver -kill :*``

To connect install [TigerVNC Client](https://tigervnc.org/) on your laptop and connect using VPN (ask CeNT IT for an account) or use the [sshuttle](first_steps.md).

TigerVNC uses ports 590x, where x is the session number. If your session is the only one it should have port 5901.
In that case if you connect using sshuttle use the following connection address in the TigerVNC client (substitute with lab0xx):
```shell
lab001.sih-59.internal:5901
```