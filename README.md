# NUT-UPS-Monitoring
Just a reminder of how NUT works and how to add slaves to monitoring

## Adding a Linux Slave Device to TrueNAS Scale NUT Service

These steps configure a Linux machine as a NUT network client (slave) monitored by a TrueNAS Scale UPS service.

### 1. Install NUT

```bash
apt update
apt install nut
```

### 2. Configure NUT mode

Edit `/etc/nut/nut.conf` and set the mode to `netclient`:

```
MODE=netclient
```

### 3. Configure UPS monitoring

Edit `/etc/nut/upsmon.conf` and add the following line, replacing `<TRUENAS_IP>` with your TrueNAS server's IP address and `<PASSWORD>` with the password configured on the TrueNAS NUT service:

```
MONITOR CyberPower@<TRUENAS_IP> 1 upsmonitor <PASSWORD> slave
```

### 4. Enable and start the NUT client service

```bash
systemctl restart nut-client
systemctl enable nut-client
```

### 5. Verify the connection

```bash
upsc CyberPower@<TRUENAS_IP>
```

If the connection is successful, this command will display the current UPS status and variables from the TrueNAS NUT server.
