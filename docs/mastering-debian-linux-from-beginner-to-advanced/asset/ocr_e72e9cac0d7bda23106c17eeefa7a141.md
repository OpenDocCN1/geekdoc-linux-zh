```
sudo apt install printer-driver-hpcups  # For HP printers
sudo apt install printer-driver-brlaser  # For Brother
printers
```

# 4. Managing print jobs:

+   - Use the print queue viewer in your desktop environment
+   - Or use command-line tools:

```
lpq  # View print queue
lprm <job-id>  # Remove a print job
```

# Scanners

+   1. SANE (Scanner Access Now Easy):

SANE is the standard scanner interface for Debian:

```
sudo apt install sane
```

+   2. Adding a scanner:

Most scanners are automatically detected. To check:

```
scanimage -L
```