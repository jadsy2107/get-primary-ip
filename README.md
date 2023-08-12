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
