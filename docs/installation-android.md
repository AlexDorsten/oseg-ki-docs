# OpenCode auf Android installieren und koppeln

[Zur README](../README.md) · Voraussetzung: [Einstiegskonfiguration](einstiegskonfiguration.md)

Stand: 20. November 2026.

## Voraussetzung

OpenCode Mobile steuert die Sessions auf deinem Computer. Richte zuerst [Linux](installation-linux.md) oder [macOS](installation-macos.md) und anschließend IFM ein. Der Rechner muss während der Nutzung laufen und erreichbar sein. Der API-Schlüssel bleibt in der Konfiguration des Rechners. [Funktionsweise und Kopplung](https://opencode.ai/mobile)

## 1. App installieren

Öffne den [offiziell verlinkten Google-Play-Eintrag](https://play.google.com/store/apps/details?id=ai.opencode.mobilecode) auf deinem Smartphone und installiere **OpenCode**. Ob dein Gerät unterstützt wird, zeigt Google Play an.

## 2. Rechner verbinden

Starte OpenCode auf dem Rechner und öffne dort eine Session im Projekt `OSEG-AI`. Führe im Terminal desselben Benutzerkontos aus:

```sh
opencode pair --remote
```

Scanne den angezeigten QR-Code mit der Android-App oder füge den Kopplungslink dort ein. Der Link ist einmal verwendbar und läuft nach fünf Minuten ab. `--remote` ermöglicht den Zugang über OpenTunnel auch aus anderen Netzwerken. Teile den Kopplungslink nur mit dem Gerät, das Zugriff bekommen soll. [Offizielle Anleitung](https://opencode.ai/mobile)

## 3. Verbindung prüfen

Öffne auf dem Smartphone die zuvor am Rechner angelegte Session. Sende beispielsweise:

> Nenne mir den Namen des geöffneten Projekts und des ausgewählten Modells.

Prüfe den Modellnamen zusätzlich in der Modellauswahl: Erwartet wird **K2 Horizon 375B-A23B (IFM)**. Eine Selbstauskunft des Modells allein bestätigt die Konfiguration nicht.

## Wenn die Kopplung scheitert

| Symptom | Nächster Schritt |
| --- | --- |
| Link abgelaufen oder schon benutzt | `opencode pair --remote` erneut ausführen. |
| Sessions fehlen | Prüfen, ob Desktop und CLI denselben Benutzer und Hintergrunddienst verwenden. |
| Verbindung bricht ab | Netzwerk und Ruhezustand des Rechners prüfen. |
| Pairing ist deaktiviert | Prüfen, ob der gemeinsame Dienst deaktiviert wurde; bei Bedarf `opencode service unset disabled` ausführen. |

Die [CLI-Dokumentation](https://opencode.ai/docs/cli/#background-service) erklärt den gemeinsamen Dienst. Bei weiteren Problemen helfen `opencode service status` und die [Fehlerhilfe](https://opencode.ai/docs/troubleshooting/).
