# Slow WSL Network

If the WSL network is running slowly, run this in an elevated PowerShell terminal:

```bash
Disable-NetAdapterLso -Name "vEthernet (WSL)"
```
