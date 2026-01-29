# NAS Cloud

<div align="center">

![NAS Cloud Logo](https://img.shields.io/badge/NAS-Cloud-blue?style=for-the-badge)
![Version](https://img.shields.io/badge/version-2.3.0-green?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-orange?style=for-the-badge)

**Modulares NAS-System mit Web-Interface und GitHub-Integration**

[Installation](#installation) • [Features](#features) • [Module](#module) • [Dokumentation](#dokumentation) • [Updates](#updates)

</div>

---

## 📖 Über das Projekt

NAS Cloud ist ein vollständig modulares Network Attached Storage (NAS) System für Debian 12, das als private Cloud-Lösung konzipiert wurde. Mit einem modernen Web-Interface, GitHub-basiertem Modul-Shop und flexibler Plugin-Architektur bietet es eine einfache Möglichkeit, eigene Storage-Lösungen zu erstellen und zu erweitern.

### ✨ Highlights

- 🎯 **Modular**: Plugin-System für maximale Flexibilität
- 🛒 **GitHub Shop**: Automatische Updates über GitHub Releases
- 🎨 **Modern UI**: Responsive Web-Interface mit Dashboard
- 👤 **User Management**: Profile, Authentifizierung, Einstellungen
- 🔧 **Erweiterbar**: Eigene Module in wenigen Minuten erstellen
- 📦 **Klein**: Basis-Installation nur 16 KB

---

## 🚀 Quick Start

### Installation (Debian 12)

```bash
# 1. Basis-System installieren
sudo dpkg -i nas-cloud_2.3.0_all.deb

# 2. Browser öffnen
http://localhost

# 3. Einloggen
Benutzername: admin
Passwort: admin
```

**Das war's!** 🎉 Das System läuft und du kannst Module installieren.

---

## 🎯 Features

### Core Features

| Feature | Beschreibung |
|---------|-------------|
| 📊 **Dashboard** | Übersicht über Speicher, Dateien und Module |
| 📁 **File Upload** | Drag & Drop Datei-Upload mit Verwaltung |
| 👤 **User Profile** | E-Mail & Passwort ändern, Einstellungen |
| 🛒 **Module Shop** | GitHub-Integration für automatische Updates |
| 🔒 **Authentication** | Session-basiertes Login-System |
| 📱 **Responsive** | Funktioniert auf Desktop, Tablet & Mobile |

### System Settings Modul

- ⚡ Live CPU & RAM Monitoring (Auto-Refresh 5s)
- 🖥️ System-Informationen (Hostname, OS, Python, Uptime)
- ⚙️ Service-Verwaltung (Start/Stop/Restart)
- 📦 Update-Manager (apt updates prüfen & installieren)

### Workflow Optimizer Modul

- 🔄 Automatische Backup-Tasks
- 🧹 Cleanup-Scheduler (Temp-Files, Logs)
- 🗄️ Datenbank-Optimierung
- 📊 Task-Historie mit Status
- ⚡ Manuelle Task-Ausführung
- 🎯 Custom Scripts

---

## 📦 Module

### Verfügbare Module

| Modul | Version | Beschreibung |
|-------|---------|--------------|
| **System Settings** | 1.1.0 | System-Überwachung & Service-Verwaltung |
| **Workflow Optimizer** | 1.1.0 | Task-Automation & Backups |
| Storage Stats | 1.0.0 | Speicherplatz-Statistiken |
| File Manager | 1.0.0 | Erweiterte Dateiverwaltung |
| User Settings | 1.0.0 | Benutzer-Profilverwaltung |
| Disk Tools | 1.0.0 | S.M.A.R.T. Monitoring |
| Network Settings | 1.0.0 | Netzwerk-Konfiguration |
| RAID Manager | 1.0.0 | RAID-Array Verwaltung |
| MergeFS Manager | 1.0.0 | Storage Pool Management |
| Emby Server | 1.0.0 | Media Server Integration |

### Module installieren

**Option 1: Über Shop (Empfohlen)**

1. Browser öffnen: `http://localhost/modules/shop`
2. Modul auswählen
3. "Installieren" klicken
4. System neu starten: `sudo systemctl restart nas-cloud`

**Option 2: Manuell hochladen**

1. Browser öffnen: `http://localhost/modules`
2. "Modul installieren" klicken
3. `.tar.gz` Datei hochladen
4. System neu starten: `sudo systemctl restart nas-cloud`

---

## 🛠️ Eigene Module entwickeln

### Modul-Struktur

```
my-module/
├── manifest.json
└── module.py
```

### manifest.json

```json
{
  "id": "my-module",
  "name": "My Awesome Module",
  "version": "1.0.0",
  "description": "Beschreibung deines Moduls",
  "author": "Dein Name"
}
```

### module.py

```python
"""My Awesome Module"""

def register_routes(app):
    from flask import jsonify, session
    
    @app.route('/api/modules/my-module/hello')
    def hello():
        if 'user_id' not in session:
            return jsonify({'error': 'Not authenticated'}), 401
        
        return jsonify({'message': 'Hello from my module!'})
```

### Modul packen & installieren

```bash
# Packen
tar czf my-module.tar.gz my-module/

# Im Browser hochladen
http://localhost/modules → "Modul installieren"

# Oder manuell kopieren
sudo tar xzf my-module.tar.gz -C /opt/nas-cloud/modules/
sudo systemctl restart nas-cloud
```

---

## 📚 Dokumentation

### System-Anforderungen

- **OS**: Debian 12 (Bookworm)
- **Python**: 3.9+
- **RAM**: Mindestens 512 MB
- **Speicher**: 100 MB für Basis-Installation
- **Ports**: Port 80 (HTTP)

### Verzeichnis-Struktur

```
/opt/nas-cloud/
├── src/
│   └── app.py              # Haupt-Applikation
├── templates/
│   ├── dashboard.html      # Dashboard
│   ├── login.html          # Login-Seite
│   ├── modules.html        # Module-Übersicht
│   ├── shop.html           # Modul-Shop
│   └── ...
├── modules/                # Installierte Module
│   ├── system-settings/
│   └── workflow-optimizer/
├── data/
│   └── nas.db             # SQLite Datenbank
└── uploads/               # Hochgeladene Dateien
```

### API-Endpunkte

#### Authentifizierung
```
POST /login              - Benutzer einloggen
GET  /logout             - Benutzer ausloggen
```

#### Dashboard & Stats
```
GET  /                   - Dashboard anzeigen
GET  /api/stats          - System-Statistiken
```

#### Module
```
GET  /api/modules        - Alle Module auflisten
POST /modules/upload     - Modul hochladen
POST /api/modules/toggle - Modul aktivieren/deaktivieren
```

#### Shop
```
GET  /api/shop/modules   - Verfügbare Module (GitHub)
POST /api/shop/install/<id> - Modul von GitHub installieren
```

#### User Profile
```
GET  /profile            - Profil-Seite anzeigen
GET  /api/profile        - Profil-Daten laden
POST /api/profile        - Profil aktualisieren
POST /api/change-password - Passwort ändern
```

---

## 🔄 Updates

### Basis-System updaten

```bash
# Alte Version entfernen
sudo dpkg -r nas-cloud

# Neue Version installieren
sudo dpkg -i nas-cloud_2.3.0_all.deb
```

### Module updaten (über Shop)

1. Shop öffnen: `http://localhost/modules/shop`
2. Module mit "Update verfügbar" Badge angezeigt
3. "Update auf v1.x.x" klicken
4. System neu starten: `sudo systemctl restart nas-cloud`

### Module manuell updaten

```bash
# Neues Modul hochladen (überschreibt alte Version)
http://localhost/modules → "Modul installieren"

# Oder per Terminal
sudo tar xzf system-settings-v1.1.0.tar.gz -C /opt/nas-cloud/modules/
sudo systemctl restart nas-cloud
```

---

## 🐛 Troubleshooting

### Service läuft nicht

```bash
# Status prüfen
sudo systemctl status nas-cloud

# Logs ansehen
sudo journalctl -u nas-cloud -n 50

# Service neu starten
sudo systemctl restart nas-cloud
```

### Webseite nicht erreichbar

```bash
# Port prüfen
sudo netstat -tlnp | grep 80

# Service läuft?
sudo systemctl status nas-cloud

# Firewall?
sudo ufw status
```

### Module laden nicht

```bash
# Module in Datenbank prüfen
sqlite3 /opt/nas-cloud/data/nas.db "SELECT * FROM modules;"

# Modul-Dateien prüfen
ls -la /opt/nas-cloud/modules/

# Logs prüfen
sudo journalctl -u nas-cloud | grep -i error
```

### Dependencies fehlen

```bash
# Flask installieren
pip3 install flask requests psutil --break-system-packages

# Service neu starten
sudo systemctl restart nas-cloud
```

---

## 🏗️ Entwicklung

### Repository klonen

```bash
git clone https://github.com/marcuswitt/modular-nas.git
cd modular-nas
```

### Lokaler Development-Server

```bash
cd /opt/nas-cloud/src
python3 app.py
```

### Tests

```bash
# Module testen
curl http://localhost/api/modules

# Shop testen
curl http://localhost/api/shop/modules

# System-Stats testen
curl -b cookies.txt http://localhost/api/stats
```

---

## 📋 Changelog

### v2.3.0 (2026-01-29)
- ✨ Modulare Architektur (Basis ohne Module)
- ✨ System Settings Modul mit Live-Monitoring
- ✨ Workflow Optimizer Modul
- ✨ User-Dropdown-Menü mit Profil
- ✨ Modul-spezifische UI-Seiten
- 🐛 Template-Pfad fix
- 📚 Vollständige Dokumentation

### v2.2.0 (2026-01-29)
- ✨ Dashboard mit Modul-Karten
- ✨ User-Profil-Seite
- ✨ Stats-API
- ✨ Modul-Detail-Seiten

### v2.1.0 (2026-01-28)
- ✨ GitHub Shop Integration
- ✨ Automatische Updates
- ✨ Modul-Katalog-System

### v2.0.0 (2026-01-28)
- ✨ Erstes modulares System
- ✨ Plugin-Architektur
- ✨ Web-Interface

---

## 🤝 Contributing

Contributions sind willkommen! 

1. Fork das Repository
2. Erstelle einen Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit deine Änderungen (`git commit -m 'Add some AmazingFeature'`)
4. Push zum Branch (`git push origin feature/AmazingFeature`)
5. Öffne einen Pull Request

### Modul beisteuern

Du hast ein cooles Modul entwickelt?

1. Modul als `.tar.gz` packen
2. Issue öffnen mit Modul-Beschreibung
3. Modul wird geprüft
4. Bei Approval: Wird in `catalog.json` aufgenommen

---

## 📄 License

Dieses Projekt ist unter der MIT License lizenziert - siehe [LICENSE](LICENSE) Datei für Details.

---

## 🙏 Credits

Entwickelt von **Marcus Witt**

### Technologien

- [Flask](https://flask.palletsprojects.com/) - Web Framework
- [SQLite](https://www.sqlite.org/) - Datenbank
- [Python 3](https://www.python.org/) - Backend
- [Vanilla JavaScript](https://javascript.info/) - Frontend
- [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github) - Module-Distribution

---

## 📞 Support

- 🐛 **Issues**: [GitHub Issues](https://github.com/marcuswitt/modular-nas/issues)
- 💬 **Discussions**: [GitHub Discussions](https://github.com/marcuswitt/modular-nas/discussions)

---

## 🗺️ Roadmap

### v2.4.0 (Q1 2026)
- [ ] Disk Tools UI komplett
- [ ] Network Settings UI
- [ ] RAID Manager UI
- [ ] Multi-User Support
- [ ] Rollen & Berechtigungen

### v2.5.0 (Q2 2026)
- [ ] MergeFS Manager UI
- [ ] Emby Server Integration
- [ ] Backup-Scheduler erweitern
- [ ] E-Mail-Benachrichtigungen
- [ ] Mobile App (Android)

### v3.0.0 (Q3 2026)
- [ ] Docker Support
- [ ] Kubernetes Deployment
- [ ] API Token Authentication
- [ ] Webhook Integration
- [ ] Plugin Marketplace

---

<div align="center">

**Made with ❤️ for the Self-Hosted Community**

⭐ Wenn dir dieses Projekt gefällt, gib ihm einen Stern!

[⬆ Back to top](#nas-cloud)

</div>
