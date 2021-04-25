NOT WORKING YET: Causes infinite loop in Ubuntu 20.04. Issue: https://github.com/DamionGans/ubuntu-wsl2-systemd-script/issues/29

# Getting k3s to work with WSL2

Source: https://worklifenotes.com/2020/09/01/running-k3s-on-windows-with-wsl2/

Steps:
1. Install WSL2: https://docs.microsoft.com/en-us/windows/wsl/install-win10
2. Recommended: Setting CPU and memory limits to WSL2:
   1. Create the following file: c:\users\<profile name>\.wslconfig
   2. Content of the file (set CPU and memory limit as desired):
    ```
    [wsl2]
    memory=4GB # Limits VM memory in WSL 2 to 4 GB
    processors=2 # Makes the WSL 2 VM use two virtual processors
    ```
   3. Restart WSL2 (LxssManager Service). Run it in Powershell with Admin rights:
   ```
   Restart-Service LxssManager
   ```
3. Install Ubuntu 20.04 from the Microsoft Store. **Warning: Install exactly this version. The method might not work for other versions.**
4. For k3s you need systemd. To make it work in WSL, follwo the steps in the following heading.
5. After systemd is working in your linux distro, install k3s (following heading)


# Getting systemd to work in WSL (Ubuntu 20.04)
Script to enable systemd support on current Ubuntu WSL2 images from the Windows store.


Get and run the script: 
```sh
git clone https://github.com/andraspatka/ubuntu-wsl2-systemd-script.git
cd ubuntu-wsl2-systemd-script/
sudo bash ubuntu-wsl2-systemd-script.sh --force
# Enter your password and wait until the script has finished
```
Restart the Ubuntu shell: close the terminal, then run:
```sh
wsl -t Ubuntu-20.04
```

and try running systemctl:
```sh
systemctl
```
If you don't get an error and see a list of units, the script worked.

# Installing k3s

Instructions can be found here: https://k3s.io/