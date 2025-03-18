# SSH File Transfer via Ethernet

## 1️⃣ Setting Up a Manual IP Address
On **Laptop 1 (Ubuntu):**
```bash
sudo ip addr add 192.168.1.1/24 dev enp0s31f6
sudo ip link set enp0s31f6 up
```

On **Laptop 2 (Kali Linux):**
```bash
sudo ip addr add 192.168.1.2/24 dev enp0s31f6
sudo ip link set enp0s31f6 up
```

🔹 **Explanation:** Assigns a static IP to the Ethernet interface and brings it up.

## 2️⃣ Verifying the Connection
On **Laptop 1:**
```bash
ping -c 4 192.168.1.2
```
On **Laptop 2:**
```bash
ping -c 4 192.168.1.1
```

🔹 **Explanation:** Sends 4 packets to verify the connection between both laptops.

## 3️⃣ Enabling SSH Service (If Not Running)
On **Laptop 2 (Target System):**
```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```

🔹 **Explanation:** Starts SSH service and enables it to launch at boot.

## 4️⃣ Connecting via SSH
From **Laptop 1:**
```bash
ssh username@192.168.1.2
```

🔹 **Explanation:** Securely logs into the remote machine over Ethernet.

## 5️⃣ Transferring Files Using SCP
From **Laptop 1 to Laptop 2:**
```bash
scp largefile.iso username@192.168.1.2:/home/username/
```

🔹 **Explanation:** Securely copies files from one system to another.

## 6️⃣ Transferring Files Using Rsync (More Efficient)
```bash
rsync -av --progress largefile.iso username@192.168.1.2:/home/username/
```

🔹 **Explanation:** Synchronizes files efficiently, showing progress.

## 7️⃣ Disconnecting SSH
Simply type:
```bash
exit
```

🔹 **Explanation:** Closes the SSH session.

## 🎉 Conclusion
This guide covers **manual IP setup, SSH access, and file transfer** over Ethernet. It's a great hands-on learning experience for networking and Linux users! 🚀
