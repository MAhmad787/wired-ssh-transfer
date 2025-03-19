# SSH File Transfer via Ethernet (Windows, Linux, macOS)

## 1️⃣ Setting Up a Manual IP Address
### **Linux:**
Identify your Ethernet interface:
```bash
ip a
```
Look for an interface like `enp0s31f6`, `eth0`, or similar. Your interface name may differ.

On **System A:**
```bash
sudo ip addr add 192.168.1.1/24 dev <your-interface>
sudo ip link set <your-interface> up
```

On **System B:**
```bash
sudo ip addr add 192.168.1.2/24 dev <your-interface>
sudo ip link set <your-interface> up
```

### **Windows (PowerShell - Admin Mode):**
Find your Ethernet interface:
```powershell
netsh interface ip show interfaces
```
Set a static IP (Example: `192.168.1.3` for System A):
```powershell
netsh interface ip set address name="Ethernet" static 192.168.1.3 255.255.255.0
```

### **macOS:**
Find your Ethernet interface:
```bash
ifconfig
```
Assign a static IP (Example: `192.168.1.1` for System A):
```bash
sudo ifconfig en0 192.168.1.1 netmask 255.255.255.0 up
```

🔹 **Explanation:** Assigns a static IP to the Ethernet interface and brings it up. Replace `<your-interface>` or `en0` with the correct name.

## 2️⃣ Verifying the Connection
On **System A:**
```bash
ping -c 4 192.168.1.2  # Linux/macOS
ping 192.168.1.2 -n 4  # Windows
```
On **System B:**
```bash
ping -c 4 192.168.1.1  # Linux/macOS
ping 192.168.1.1 -n 4  # Windows
```

🔹 **Explanation:** Sends 4 packets to verify the connection between both systems.

## 3️⃣ Enabling SSH Service (If Not Running)
### **Linux (Receiving System):**
```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```
### **Windows (Enable OpenSSH Server):**
```powershell
Start-Service sshd
Set-Service -Name sshd -StartupType Automatic
```
Allow SSH through the firewall:
```powershell
netsh advfirewall firewall add rule name="OpenSSH" dir=in action=allow protocol=TCP localport=22
```
### **macOS:**
Enable Remote Login (SSH):
```bash
sudo systemsetup -setremotelogin on
```

## 4️⃣ Connecting via SSH
From **System A:**
```bash
ssh username@192.168.1.2
```
🔹 **Explanation:** Securely logs into the remote machine over Ethernet.

## 5️⃣ Transferring Files Using SCP
### **Linux/macOS to Another System:**
```bash
scp largefile.iso username@192.168.1.2:/path/to/destination/
```
### **Windows to Another System (PowerShell):**
```powershell
scp C:\Users\username\Desktop\largefile.iso username@192.168.1.2:/path/to/destination/
```
🔹 **Explanation:** Securely copies files from one system to another.

## 6️⃣ Transferring Files Using Rsync (More Efficient)
### **Linux/macOS:**
```bash
rsync -av --progress largefile.iso username@192.168.1.2:/path/to/destination/
```
### **Windows (Using WSL or Cygwin):**
```bash
rsync -av --progress /mnt/c/Users/username/Desktop/largefile.iso username@192.168.1.2:/path/to/destination/
```
🔹 **Explanation:** Synchronizes files efficiently, showing progress.

## 7️⃣ Disconnecting SSH
Simply type:
```bash
exit
```
🔹 **Explanation:** Closes the SSH session.

## ℹ️ Additional Notes
- **Interface Names Vary:** Your Ethernet interface might have a different name (`eth0`, `enpXsY`, `Ethernet`, `en0`, etc.). Always check using `ip a` (Linux), `ipconfig` (Windows), or `ifconfig` (macOS).
- **Windows Compatibility:** SSH and SCP work on Windows if OpenSSH is installed, but rsync may require `WSL` or `Cygwin`.
- **File Paths:** Ensure correct paths while transferring files. Absolute paths work best.

## 🎉 Conclusion
This guide covers **manual IP setup, SSH access, and file transfer** over Ethernet for Linux, Windows, and macOS. A great way to practice networking fundamentals and system administration! 🚀
