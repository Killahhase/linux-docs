[Back to index](./index.md)

## General commands

### changing system hostname

```bash
echo "192.168.18.50 myhost.example.com" | sudo tee -a /etc/hosts
sudo hostnamectl set-hostname myhost.example.com
```

Replace myhost.example.com with your correct hostname/valid domain name.
In a local environment behind a fritz.box router, this would be `myhost.fritz.box`.