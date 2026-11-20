# OpenCode Desktop unter macOS installieren

[Zur README](../README.md) · Weiter: [Einstiegskonfiguration](einstiegskonfiguration.md)

Stand: 20. November 2026. Ziel: OpenCode **2.x**, Desktop und CLI unter demselben macOS-Benutzerkonto.

## 1. Desktop-App installieren

Wähle einen der beiden Wege.

### Direkter Download

1. Öffne im Apple-Menü „Über diesen Mac“. Bei einem Apple-Chip wähle **Apple Silicon**, bei einem Intel-Prozessor **Intel**.
2. Lade die passende Version von der [offiziellen OpenCode-Desktopseite](https://opencode.ai/desktop).
3. Öffne das heruntergeladene Installationsabbild und ziehe OpenCode in den Ordner „Programme“.
4. Starte OpenCode aus „Programme“ und öffne den lokalen Projektordner `OSEG-AI`.

### Mit vorhandenem Homebrew

Der auf der Desktopseite veröffentlichte Installationsbefehl lautet:

```sh
brew install --cask opencode-desktop
```

Starte danach OpenCode aus „Programme“. Wenn du Homebrew nicht verwendest, genügt der direkte Download.

## 2. CLI für Prüfung und Smartphone-Kopplung ergänzen

Prüfe im Terminal, ob der Befehl bereits vorhanden ist:

```sh
opencode --version
```

Fehlt er, installiere die aktuelle V2-CLI. Mit Homebrew:

```sh
brew install anomalyco/tap/opencode-v2
```

Alternativ ohne Homebrew:

```sh
curl -fsSL https://opencode.ai/v2/install | bash
```

Verwende nur einen Installationsweg für die CLI. Öffne nach der Installation ein neues Terminal und prüfe `opencode --version`. Erwartet wird **2.x**. Die CLI-Befehle stammen aus der [aktuellen OpenCode-Installationsanleitung](https://opencode.ai/docs/).

## 3. Installation prüfen

- Die Desktop-App startet und öffnet den Projektordner.
- `opencode --version` meldet Version 2.x.
- Im Terminal lässt sich im Projektordner mit `opencode` eine Session öffnen.

Nun folgt die [Einstiegskonfiguration für IFM](einstiegskonfiguration.md). Sie verwendet eine Schlüsseldatei, die auch beim Start der App aus Finder oder Dock verfügbar ist.

## Aktualisieren

Bei einer Homebrew-Installation:

```sh
brew update
brew upgrade --cask opencode-desktop
brew upgrade anomalyco/tap/opencode-v2
```

Führe nur die Upgrade-Befehle für Komponenten aus, die du über Homebrew installiert hast. Beim direkten Desktop-Download lade die neue Version erneut von der offiziellen Seite. Halte Desktop und CLI auf einem zueinander passenden Versionsstand.
