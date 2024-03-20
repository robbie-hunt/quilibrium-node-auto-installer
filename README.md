

## This is a script to auto-install your Quilibrium node in the easieast way. Not tested yet, use at your own risk!

 1. Run the auto-installer script on your server (OS must be Ubuntu 22.04.X)
```
 wget -O - https://raw.githubusercontent.com/lamat1111/quilibrium-node-auto-installer/3621cad16d203c8a5806d4a7484dd901281f705e/installer | bash
```
 2. After installing the node and making some necessary edits, the script will run your node for 5 minutes and then you will be prompted to reboot the system, type "Y" and reboot.
 3. Login again in your server.
 4. Go to the node folder, create a persistent shell (session) and run the poor_mans_cd script. To do all this run these commands one after the other.
```
cd ceremonyclient/node 
```

```
tmux new-session -s quil 
```

```
./poor_mans_cd.sh
```

To detach from tmux press CTRL+B then D and ENTER. Now you can safely logout from your server and the node will keep running in its persistent shell.

To reattach later to the node session run the following `tmux a -t quil`
The poor_mans_cd script will also restart your node if it gets killed and will auto-update it when there is a new version available.


Your node will automatically generate important key and config files. After your node has been running for a while, remember to back these files up. You can find them in the ceremonyclient/node/.store folder: keys.yml and config.yml. Keep these safe and do not share them with anyone. 

An easy client to download files from your node on Windows is [WinSCP](https://winscp.net/eng/index.php). You will need to show hidden files. Select Options, Preferences from the main menu, then the Panels tab, and check the option to Show hidden files (Ctrl+Alt+H).

## Resources
 - To manage your nodes use [Termius](https://termius.com/), the coolest SSH client and terminal around :) 
 - To track your server uptime and  resources usage use [Hetrixtools.com](https://hetrixtools.com/), you can track up to 15 servers for free and the setup is very easy

## Useful server commands

Check node version
```bash
grep -o -P 'Node -.{0,8}' ~/ceremonyclient/node/main.go
```

Get node peer ID
```bash
cd ~/ceremonyclient/node && GOEXPERIMENT=arenas go run ./... -peer-id
```

Check QUIL balance
```bash
cd ~/ceremonyclient/node && GOEXPERIMENT=arenas /root/go/bin/node -balance
```

Attach to existing tmux session
```bash
tmux a -t quil
#To detach from tmux press CTRL+B then release both keys and press D 
```

Move keys.yml and config.yml to new server
```bash
scp -f /root/ceremonyclient/node/.config/keys.yml /root/ceremonyclient/node/.config/config.yml root@<NEW_SERVER_IP>:/root/ceremonyclient/node/.config/
```
