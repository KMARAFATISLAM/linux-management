### 1. Allow SSH Access

```
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

**Reason**: This rule allows incoming SSH connections on the standard port 22.

**Why**: Without this rule, remote management would be impossible if the default policy is set to DROP.

### 2. Allow Established and Related Connections

```
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

**Reason**: This rule permits packets that are part of established connections or related to existing connections.

**Why**: For proper network functionality, the server needs to receive responses to outgoing connections. This rule ensures that ongoing connections are not disrupted by the firewall.

### 3. Set Default Policy for Outgoing Traffic

```
sudo iptables -P OUTPUT ACCEPT
```

**Reason**: Sets the default rule for outbound traffic to accept.

**Why**: This allows the server to start outgoing connections without restrictions, which is generally safe since the rule focuses on incoming traffic.

### 4. Allow HTTP Traffic

```
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

**Reason**: Permits incoming HTTP connections on the standard port 80.

**Why**: Necessary for a web server, allowing users to access web content hosted on the server.

### 5. Allow HTTPS Traffic

```
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

**Reason**: Allows incoming HTTPS connections on the standard port 443.

**Why**: Required for secure web communications through SSL, enabling encrypted data transfer between clients and the server.

### 6. SYN Flood Protection

```
sudo iptables -A INPUT -p tcp --syn -m limit --limit 1/s --limit-burst 3 -j ACCEPT
sudo iptables -A INPUT -p tcp --syn -j DROP
```

**Reason**: Limits the rate of new TCP connections with the SYN flag and drops excessive requests.

**Why**: Protects against SYN flood attacks, which attempt to consume server resources by sending a large number of SYN packets without completing the TCP handshake.

### 7. NULL Packet Protection

```
sudo iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP
```

**Reason**: Drops packets with no TCP flags set (NULL packets).

**Why**: NULL packets are often used in network reconnaissance and can indicate a port scan. Legitimate traffic should never have all TCP flags unset, making this an effective rule to block certain types of scanning activity.

### 8. Log Blocked Traffic

```
sudo iptables -A INPUT -j LOG --log-prefix "BLOCKED: "
```

**Reason**: Logs all packets that reach this rule.

**Why**: Provides visibility into blocked traffic, aiding in threat analysis and firewall rule optimization.

### 9. Log New Allowed Connections

```
sudo iptables -I INPUT 1 -m state --state NEW -j LOG --log-prefix "ALLOWED: "
```

**Reason**: Logs all new connections that are allowed through the firewall.

**Why**: Helps monitor legitimate traffic and detect anomalies in access patterns, valuable for security auditing.

### 10. Save Firewall Rules

```
sudo iptables-save > /etc/iptables.rules
sudo iptables-save | sudo tee /etc/iptables.rules > /dev/null
```

**Reason**: Saves the current iptables configuration to a file.

**Why**: Ensures rules can be restored after a system reboot.

### 11. Restore Rules at Boot

```
sudo sh -c "echo 'iptables-restore < /etc/iptables.rules' >> /etc/rc.local"
sudo chmod +x /etc/rc.local
```

**Reason**: Configures the system to restore iptables rules on boot.

**Why**: Ensures continuous protection even after server restarts.