# Server Migration – Hetzner Dedicated Server

## 1. Ausgangslage

### Alter Server (eigentlich noch ziemlich neu)
- **Anbieter:** Hetzner Dedicated Server  
- **Betriebssystem:** Proxmox VE 9  
- **Hardware:** AMD Ryzen 7 Pro 8700GE, 64 GB RAM, 2× 512 GB NVMe  
- **Dienste:** Mailserver, Websites, TeamSpeak-Server, Gameserver und weitere öffentlich erreichbare Services  

### Neuer Server
- **Anbieter:** Hetzner Dedicated Server  
- **Betriebssystem:** Proxmox VE 9  
- **Hardware:** Intel Core i9-9900K, 128 GB RAM, 2× 1 TB NVMe  
- **Aufbau:** identisch zum alten Server  

---

## 2. Planung

Der ursprüngliche Plan war:
- Den alten Server komplett zu Hause zu sichern  
- Auf dem neuen Server alles wiederherzustellen  
- Wunsch war ein Upgrade über **Hetzner Upgrade Option 4**, wurde jedoch nicht ermöglicht  
- Stattdessen erfolgte die Migration manuell  

---

## 3. Einrichtung des neuen Servers

- Initial gab es Stabilitätsprobleme: Server stürzte mehrfach ab  
- **Troubleshooting** gemeinsam mit dem Hetzner-Support → beide NVMe-SSDs wurden getauscht  
- Installation von **Proxmox VE 9** per KVM-Konsole  
- Netzwerk mit **pfSense** übernommen (PCIe Passthrough des Netzwerkcontrollers)  

---

## 4. Migration

- Backups aller wichtigen Daten und Services lokal erstellt  
- Übertragung per **SCP** auf den neuen Server  
- Wiederherstellung der Services in Proxmox-Umgebungen  
- Besonderer Fokus: **Mailserver** möglichst lange online gehalten  
- Migration erfolgte abends, um Downtime gering zu halten  
- Hetzner übernahm die **alte IP-Adresse** auf den neuen Server → keine DNS-Anpassungen notwendig  

---

## 5. Nacharbeiten

- Backups erneut eingerichtet  
- E-Mail-Benachrichtigungen konfiguriert  
- Storages angebunden:
  - Proxmox Backup Server  
  - Hetzner Storage Box  

---

## 6. Lessons Learned

- Migration lief insgesamt reibungslos  
- Einziger großer Zeitfresser: **~4 Stunden Troubleshooting** wegen defekter NVMe-SSDs  
- Vorteil: durch IP-Übernahme musste kein DNS umgestellt werden  
- Zukünftig: vorab Hardwaretests einplanen, um ähnliche Probleme zu vermeiden  

---