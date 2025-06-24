# frida-server-ios-install

A simple guide to install Frida Server (v16.7.10) on a jailbroken iPhone 7 (arm64).

## Prerequisites

* Jailbroken iPhone (arm64)
* SSH/SCP access as `root`
* Frida tools (v16.7.10) installed on host

## Installation

1. **Download the `.deb`**

   ```bash
   curl -LO https://github.com/frida/frida/releases/download/16.7.10/frida_16.7.10_iphoneos-arm64.deb
   ```

2. **Transfer to device**

   ```bash
   scp frida_16.7.10_iphoneos-arm64.deb root@<IP>:/tmp/
   ```

3. **Install on device**

   ```bash
   ssh root@<IP> "dpkg -i /tmp/frida_16.7.10_iphoneos-arm64.deb"
   ```

4. **Start the server**

   ```bash
   ssh root@<IP> "nohup frida-server"
   ```

5. **Verify**

   * On device:

     ```bash
     netstat -an | grep 27042
     ```
   * On host:

     ```bash
     frida-ps -Uai
     ```

## Troubleshooting

* **Permission denied**: ensure `/usr/sbin/frida-server` is executable:

  ```bash
  chmod +x /usr/sbin/frida-server
  ```
* **Bad CPU type**: verify binary architecture:

  ```bash
  file /usr/sbin/frida-server
  ```
* **Version mismatch**: match both host and server to v16.7.10

