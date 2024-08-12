# Linxdot ChirpStack Gateway Installation Guide

This guide provides step-by-step instructions on how to re-purpose a Linxdot device, originally designed for Helium mining, into a standard ChirpStack gateway.

## Reflashing the Linxdot Device

### Step 1: Download the Reflashing Tool

First, download the factory tool installer required for reflashing the Linxdot device:

```bash
wget https://github.com/livinghuang/chirpstack_linxdot/raw/main/Linxdot-Factory-tool-Installer.zip
```

### Step 2: Flash the OpenWRT Image

Next, download the OpenWRT image and flash it onto the Linxdot device:

```bash
wget https://github.com/livinghuang/chirpstack_linxdot/raw/main/linxdot-opensource-image-1.0.1.tar.gz
```

## Installing ChirpStack on the Linxdot Device

### Step 1: SSH into the Linxdot Device

Use the default credentials to SSH into the Linxdot device:

- **Username**: `root`
- **Password**: `linxdot`

### Step 2: Download the ChirpStack Docker Package

Clone the ChirpStack Docker repository to set up the necessary services:

```bash
git clone https://github.com/chirpstack/chirpstack-docker.git
```

### Step 3: Start ChirpStack Services

Navigate to the `chirpstack-docker` directory and start the ChirpStack services using Docker Compose:

```bash
cd chirpstack-docker
docker-compose up
```

### Step 4: Verify ChirpStack Services

Check the status of the ChirpStack services to ensure they are running:

```bash
docker ps
```

### Step 5: Copy Configuration Files

Clone the Linxdot configuration repository and move the necessary files:

```bash
git clone https://github.com/livinghuang/linxdot.git

mv ~/linxdot/docker-compose.yml ~/chirpstack-docker/
mv ~/linxdot/global_conf.json.sx1250 /etc/lora/
mv ~/linxdot/lrpkfw /etc/init.d/
mv ~/linxdot/chirpstack /etc/init.d/
```

### Step 6: Manage ChirpStack and Lrpkfw Services

Make the management scripts executable:

```bash
chmod +x /etc/init.d/chirpstack
chmod +x /etc/init.d/lrpkfw
```

Enable the services to start on boot:

```bash
/etc/init.d/chirpstack enable
/etc/init.d/lrpkfw enable
```

### Step 7: Test the Services

Test the service management scripts to ensure they work correctly:

```bash
/etc/init.d/chirpstack stop
/etc/init.d/chirpstack start
/etc/init.d/lrpkfw start
```