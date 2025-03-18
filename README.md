# SSH File Transfer via Ethernet

## 1️⃣ Setting Up a Manual IP Address
Identify your Ethernet interface by running:
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

🔹 **Explanation:** Assigns a static IP to the Ethernet interface and brings it up. Replace `<your-interface>` with the correct name.

## 2️⃣ Verifying the Connection
On **System A:**
```bash
ping -c 4 192.168.1.2
```
On **System B:**
```bash
ping -c 4 192.168.1.1
```

🔹 **Explanation:** Sends 4 packets to verify the connection between both systems.

## 3️⃣ Enabling SSH Service (If Not Running)
On **System B (Receiving System):**
```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```

🔹 **Explanation:** Starts SSH service and enables it to launch at boot. **Windows users** need to install an OpenSSH server for this to work.

## 4️⃣ Connecting via SSH
From **System A:**
```bash
ssh username@192.168.1.2
```

🔹 **Explanation:** Securely logs into the remote machine over Ethernet.

## 5️⃣ Transferring Files Using SCP
From **System A to System B:**
```bash
scp largefile.iso username@192.168.1.2:/path/to/destination/
```

🔹 **Explanation:** Securely copies files from one system to another.

## 6️⃣ Transferring Files Using Rsync (More Efficient)
```bash
rsync -av --progress largefile.iso username@192.168.1.2:/path/to/destination/
```

🔹 **Explanation:** Synchronizes files efficiently, showing progress.

## 7️⃣ Disconnecting SSH
Simply type:
```bash
exit
```

🔹 **Explanation:** Closes the SSH session.

## ℹ️ Additional Notes
- **Interface Names Vary:** Your Ethernet interface might have a different name (`eth0`, `enpXsY`, etc.). Always check using `ip a`.
- **Windows Compatibility:** SSH and SCP work on Windows if OpenSSH is installed, but rsync may require additional setup (e.g., `Cygwin` or `WSL`).
- **File Paths:** Ensure correct paths while transferring files. Absolute paths work best.

## 🎉 Conclusion
This guide covers **manual IP setup, SSH access, and file transfer** over Ethernet. A great way to practice networking fundamentals and Linux system administration! 🚀
