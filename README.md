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

# Linxdot ChirpStack 網關安裝指南

本指南提供如何將原本設計用於 Helium 採礦的 Linxdot 設備重新配置為標準 ChirpStack 網關的步驟說明。

## 重刷 Linxdot 設備

### 步驟 1：下載重刷工具

首先，下載重刷 Linxdot 設備所需的工廠工具安裝程式：

```bash
wget https://github.com/livinghuang/chirpstack_linxdot/raw/main/Linxdot-Factory-tool-Installer.zip
```

### 步驟 2：刷入 OpenWRT 映像檔

接下來，下載 OpenWRT 開源映像檔並將其刷入 Linxdot 設備：

```bash
wget https://github.com/livinghuang/chirpstack_linxdot/raw/main/linxdot-opensource-image-1.0.1.tar.gz
```

## 安裝 ChirpStack 到 Linxdot 設備

### 步驟 1：SSH 連線到 Linxdot 設備

使用以下默認的登入資訊來 SSH 連線到 Linxdot 設備：

- **使用者名稱**：`root`
- **密碼**：`linxdot`

### 步驟 2：下載 ChirpStack Docker 套件

克隆 ChirpStack Docker 儲存庫以設置必要的服務：

```bash
git clone https://github.com/chirpstack/chirpstack-docker.git
```

### 步驟 3：啟動 ChirpStack 服務

進入 `chirpstack-docker` 目錄，並使用 Docker Compose 啟動 ChirpStack 服務：

```bash
cd chirpstack-docker
docker-compose up
```

### 步驟 4：確認 ChirpStack 服務狀態

檢查 ChirpStack 服務的狀態，以確保其正常運行：

```bash
docker ps
```

### 步驟 5：複製配置檔案

克隆 Linxdot 配置儲存庫並移動所需的檔案：

```bash
git clone https://github.com/livinghuang/linxdot.git

mv ~/linxdot/docker-compose.yml ~/chirpstack-docker/
mv ~/linxdot/global_conf.json.sx1250 /etc/lora/
mv ~/linxdot/lrpkfw /etc/init.d/
mv ~/linxdot/chirpstack /etc/init.d/
```

### 步驟 6：管理 ChirpStack 和 Lrpkfw 服務

使管理腳本具備執行權限：

```bash
chmod +x /etc/init.d/chirpstack
chmod +x /etc/init.d/lrpkfw
```

啟用服務使其在開機時自動啟動：

```bash
/etc/init.d/chirpstack enable
/etc/init.d/lrpkfw enable
```

### 步驟 7：測試服務

測試服務管理腳本以確保其正常運作：

```bash
/etc/init.d/chirpstack stop
/etc/init.d/chirpstack start
/etc/init.d/lrpkfw start
```