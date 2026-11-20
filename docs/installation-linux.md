# OpenCode Desktop unter Linux installieren

[Zur README](../README.md) · Weiter: [Einstiegskonfiguration](einstiegskonfiguration.md)

Stand: 20. November 2026. Ziel: OpenCode **2.x**, Desktop und CLI unter demselben Linux-Benutzerkonto.

## 1. Passendes Paket auswählen

Öffne die [offizielle Desktop-Downloadseite](https://opencode.ai/desktop). OpenCode bietet `.deb`, `.rpm` und AppImage jeweils für x64 und ARM64 an.

Prüfe im Terminal die Architektur:

```sh
uname -m
```

| Ausgabe | Download |
| --- | --- |
| `x86_64` | x64 |
| `aarch64` oder `arm64` | ARM64 |

Für dieses IFM-Setup wird keine lokale Modell-GPU benötigt. Du brauchst eine grafische Linux-Sitzung und eine Internetverbindung.

## 2. Desktop-App installieren

Wähle **eine** der folgenden Varianten. Die Befehle setzen voraus, dass du die heruntergeladene Datei im Ordner `~/Downloads` wie angegeben umbenannt hast. Passe den Pfad an, falls dein Downloadordner anders heißt.

### Debian, Ubuntu und darauf basierende Systeme

Lade das passende `.deb` herunter und benenne es in `opencode.deb` um:

```sh
cd ~/Downloads
sudo apt install ./opencode.deb
```

### Fedora und andere Systeme mit DNF

Lade das passende `.rpm` herunter und benenne es in `opencode.rpm` um:

```sh
cd ~/Downloads
sudo dnf install ./opencode.rpm
```

### AppImage

Lade das passende AppImage herunter und benenne es in `OpenCode.AppImage` um:

```sh
cd ~/Downloads
chmod +x OpenCode.AppImage
./OpenCode.AppImage
```

Ein AppImage lässt sich ohne Paketinstallation starten. Bei Meldungen zu fehlenden Systembibliotheken verwende die Hinweise deiner Distribution oder das passende `.deb`-/`.rpm`-Paket.

Starte die installierte App über das Anwendungsmenü; beim AppImage über die Datei. Öffne darin den lokalen Ordner `OSEG-AI`.

## 3. CLI für Prüfung und Smartphone-Kopplung ergänzen

Prüfe zunächst, ob der Befehl bereits verfügbar ist:

```sh
opencode --version
```

Ist keine CLI vorhanden, installiere sie mit dem aktuellen offiziellen **V2-Installer**:

```sh
curl -fsSL https://opencode.ai/v2/install | bash
```

Öffne danach ein neues Terminal und prüfe erneut `opencode --version`. Verwende eine `2.x`-Version passend zur Desktop-App. Der Installer setzt `curl` und `bash` voraus; alternativ stehen auf der [offiziellen Installationsseite](https://opencode.ai/docs/) eigenständige CLI-Binärdateien bereit.

## 4. Installation prüfen

- Die Desktop-App startet und öffnet den Projektordner.
- `opencode --version` meldet Version 2.x.
- Im Terminal lässt sich im Projektordner mit `opencode` eine Session öffnen.

Nun folgt die [Einstiegskonfiguration für IFM](einstiegskonfiguration.md). Danach kannst du [Android koppeln](installation-android.md).

Für spätere Aktualisierungen verwende denselben Installationsweg und halte Desktop und CLI auf einem zueinander passenden Versionsstand. Die [OpenCode-Fehlerhilfe](https://opencode.ai/docs/troubleshooting/) erklärt die Prüfung des Hintergrunddienstes.
