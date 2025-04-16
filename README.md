# Guía paso a paso para instalar y usar SYSLINUX

SYSLINUX es un conjunto de bootloaders ligeros diseñados para arrancar sistemas Linux desde dispositivos FAT como USBs, discos duros y más.

## 📦 Requisitos

- Una distribución Linux (Debian, Ubuntu, etc.)
- Acceso a sudo
- Una memoria USB (opcional, si deseas crear un medio booteable)

---

## 🛠️ Instalación de SYSLINUX

### 1. Instala `syslinux`:

```bash
sudo apt update
sudo apt install syslinux
