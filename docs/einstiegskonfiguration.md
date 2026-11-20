# Einstieg: OpenCode 2 mit K2 Horizon über IFM

[Zur README](../README.md) · Danach optional: [Android koppeln](installation-android.md)

Stand: 20. November 2026. Voraussetzung: installierte Desktop-App und CLI in Version **2.x**, ein lokaler Projektordner sowie ein IFM-Konto.

## 1. IFM-Schlüssel erstellen

Erstelle unter [IFM Platform – API Keys](https://platform.ifm.ai/api-keys) einen API-Schlüssel. Die [IFM-Kurzanleitung](https://docs.ifm.ai/docs/quickstart.md) beschreibt den Zugang zur gehosteten API.

| Einstellung | Wert |
| --- | --- |
| API-Basis | `https://api.ifm.ai/v1` |
| Modell-ID bei IFM | `IFM/K2-Horizon-375B-A23B` |
| Lokaler Modellname in dieser Vorlage | `ifm/k2-horizon` |

## 2. Schlüssel lokal speichern

Lege auf dem Rechner eine Schlüsseldatei außerhalb des Repositorys an. Die folgenden Befehle funktionieren unter Linux und macOS:

```sh
mkdir -p ~/.config/opencode/secrets
chmod 700 ~/.config/opencode/secrets
touch ~/.config/opencode/secrets/ifm-api-key
chmod 600 ~/.config/opencode/secrets/ifm-api-key
nano ~/.config/opencode/secrets/ifm-api-key
```

Füge in `nano` ausschließlich den Schlüssel als einzelne Zeile ein, ohne Anführungszeichen oder `export`. Speichere mit `Strg+O`, bestätige mit Enter und beende mit `Strg+X`. Falls `nano` fehlt, nutze einen vorhandenen Texteditor.

Die Vorlage lädt die Datei über `{file:~/.config/opencode/secrets/ifm-api-key}`. Damit hängt der Zugang nicht von einer im Terminal gesetzten Umgebungsvariablen ab. [OpenCode: Dateiinhalte einsetzen](https://opencode.ai/docs/config/#files)

## 3. Konfiguration übernehmen

Öffne ein Terminal **im Stammordner dieses Repositorys**. Prüfe, ob bereits eine globale Konfiguration vorhanden ist:

```sh
ls ~/.config/opencode/opencode.json ~/.config/opencode/opencode.jsonc
```

Meldungen über nicht vorhandene Dateien sind bei einer Erstinstallation normal. Wenn **keine** der beiden Dateien existiert, kopiere die [Vorlage](../examples/opencode.ifm.json):

```sh
cp -n examples/opencode.ifm.json ~/.config/opencode/opencode.json
```

Existiert bereits eine Konfiguration, sichere sie zuerst. Übernimm anschließend **aus der Vorlage in deine vorhandene Datei** den `ifm`-Eintrag unter `providers` sowie auf Wunsch den Standard `"model": "ifm/k2-horizon"`. Behalte andere Provider und Einstellungen bei. Verwende eine globale Konfigurationsdatei, statt dieselben Einstellungen parallel in JSON und JSONC zu pflegen.

OpenCode liest globale Einstellungen unter `~/.config/opencode/`; Projekt- und verwaltete Einstellungen können sie überlagern. [Konfigurationsorte](https://opencode.ai/docs/config/#locations)

## 4. Einstellungen verstehen

Die Vorlage verwendet das aktuelle V2-Format mit `providers`, `package` und `settings`. Die [IFM-Anleitung](https://docs.ifm.ai/docs/opencode.md) enthält noch das ältere Format; mische beide Schreibweisen nicht innerhalb eines Provider-Eintrags.

| Feld in der Vorlage | Zweck |
| --- | --- |
| `modelID` | Übermittelt die vollständige IFM-Modell-ID trotz des kürzeren lokalen Namens. |
| `reasoningField` und `requireReasoning` | Erhalten `reasoning_content` in Folgeschritten, auch bei leerem Inhalt. |
| `maxTokensField` | Verwendet das von IFM dokumentierte Feld `max_tokens`. |
| `reasoning_effort: high` | Setzt den von IFM unterstützten Reasoning-Aufwand. |
| `temperature: 1.0`, `top_p: 0.95` | Verwendet die empfohlenen IFM-Samplingwerte. |
| `input: [text]`, `tools: true` | Deklariert Textverarbeitung und Werkzeugaufrufe. |
| `limit` | Begrenzt dieses Einstiegsprofil auf 200.000 Kontext- und 32.768 Ausgabetokens. |

Die Kontextgrenze ist eine bewusst kleinere Vorgabe für den Einstieg, keine Angabe zur maximalen Modellkapazität. IFM nennt für das große K2-Horizon-Modell 512K Kontext. Lange Gespräche erhöhen den Tokenverbrauch; aktuelle Kontingente stehen bei [IFM](https://docs.ifm.ai/docs/limits.md).

Quellen: [OpenCode-Provider](https://opencode.ai/docs/providers/#custom), [Modelle und Kompatibilität](https://opencode.ai/docs/models/#compatibility), [IFM-API-Parameter](https://docs.ifm.ai/docs/chat-completions.md), [K2 Horizon](https://docs.ifm.ai/docs/introduction.md), [Reasoning bei Folgeschritten](https://docs.ifm.ai/docs/multi-turn.md).

## 5. Modell auswählen und testen

Öffne das Projekt in OpenCode Desktop und starte eine neue Session. Wähle **K2 Horizon 375B-A23B (IFM)** in der Modellauswahl. Im Terminal erreichst du die Auswahl mit `/models` innerhalb einer laufenden `opencode`-Session.

Wenn die neue Konfiguration nicht erscheint, beende laufende Aufgaben, starte mit `opencode service restart` den Hintergrunddienst neu und öffne das Projekt erneut. [Dienst prüfen](https://opencode.ai/docs/troubleshooting/#check-the-background-service)

Teste anschließend in **derselben Session**:

1. „Lies die README.md dieses Projekts mit deinem Dateilesewerkzeug und fasse den Zweck in drei Sätzen zusammen.“
2. „Lies jetzt docs/installation-android.md und erkläre anhand der Datei, welche Rolle der Rechner bei der Smartphone-Nutzung hat.“
3. „Erstelle .scratch/opencode-einstieg.md mit einer kurzen Zusammenfassung unseres Tests. Lies die Datei danach erneut und prüfe ihren Inhalt.“

Erteile die für diese Aufgaben angezeigten Werkzeugfreigaben. Prüfe die protokollierten Dateioperationen und die erzeugte Datei selbst. So werden mehrere Werkzeugschritte und eine Dateischreiboperation geprüft; die Testdatei bleibt im von Git ignorierten Arbeitsordner. Eine einfache Chatantwort allein prüft diesen Ablauf nicht.

## 6. Typische Probleme

| Problem | Prüfen |
| --- | --- |
| Modell fehlt in der Auswahl | Version 2.x, Dateipfad, JSON-Syntax und überlagernde Projektkonfiguration prüfen. |
| `401` | Schlüsseldatei vorhanden, lesbar und mit gültigem Schlüssel befüllt? |
| `403` | Ist der Schlüssel für das Modell freigeschaltet? |
| `404` | API-Basis und vollständige `modelID` mit der Vorlage vergleichen. |
| Fehler ab dem zweiten Werkzeugschritt | Reasoning-Einstellungen mit der Vorlage vergleichen. |
| `429` | Kontingent prüfen und die vom Dienst angegebene Wartezeit beachten. |

Für HTTP-Fehler gelten die [IFM-Fehlerbeschreibungen](https://docs.ifm.ai/docs/errors.md). Prüfe bei Verbindungsproblemen auch `opencode service status` und die [OpenCode-Fehlerhilfe](https://opencode.ai/docs/troubleshooting/).

Nach einem erfolgreichen Test kannst du die [Android-App koppeln](installation-android.md). Diese Vorlage wurde anhand der Herstellerdokumentation erstellt; ein erfolgreicher Live-Test mit deinem Schlüssel muss auf deinem Rechner erfolgen.
