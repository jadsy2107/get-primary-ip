# get-primary-ip
Simple bash script to determine primary IP address using ip addr and netstat -rn

```bash
#!/bin/bash

# Get the default gateway interface
gateway_interface=$(netstat -rn | awk '$1 == "0.0.0.0" {print $8}')

# Get the IP address for that interface using 'ip addr'
primary_ip=$(ip addr show $gateway_interface | grep 'inet ' | awk '{print $2}' )

echo "Primary IP Address: $primary_ip"
```

or in python:

```python
import subprocess

# Get the default gateway interface
gateway_interface_cmd = "netstat -rn | awk '$1 == \"0.0.0.0\" {print $8}'"
gateway_interface = subprocess.getoutput(gateway_interface_cmd).strip()

# Get the IP address for that interface using 'ip addr'
primary_ip_cmd = f"ip addr show {gateway_interface} | grep 'inet ' | awk '{{print $2}}' | cut -d'/' -f1"
primary_ip = subprocess.getoutput(primary_ip_cmd).strip()

print(f"Primary IP Address: {primary_ip}")
```
