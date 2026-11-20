# OSEG-AI

Dokumentation zur Nutzung von KI bei OSEG. Das Repository sammelt nachvollziehbare Anleitungen und Konfigurationsbeispiele. Der erste praktische Einstieg ist **OpenCode 2 mit K2 Horizon über die IFM-API**.

## Einstieg

| Schritt | Anleitung |
| --- | --- |
| 1a | [OpenCode Desktop unter Linux installieren](docs/installation-linux.md) |
| 1b | [OpenCode Desktop unter macOS installieren](docs/installation-macos.md) |
| 2 | [K2 Horizon und IFM einrichten](docs/einstiegskonfiguration.md) |
| 3, optional | [Android-App installieren und koppeln](docs/installation-android.md) |

Wähle in Schritt 1 dein Betriebssystem. Die [Konfigurationsvorlage](examples/opencode.ifm.json) wird in Schritt 2 erklärt.

OpenCode arbeitet auf deinem Rechner mit den Projektdateien. In diesem Setup beantwortet K2 Horizon die Modellanfragen über die gehostete IFM-API. Die Android-App bedient die Sessions auf dem Rechner aus der Ferne. Dateien, die der Agent als Kontext verwendet, können dabei an IFM übermittelt werden; dieses Setup führt das Modell nicht lokal aus. [IFM-API](https://docs.ifm.ai/docs/quickstart.md), [OpenCode Mobile](https://opencode.ai/mobile)

## Projektstand

Die Anleitungen beschreiben einen technischen Einstieg. Entscheidungen über eine vereinsweite Nutzung werden gesondert getroffen.

Die Anleitungen wurden am **20. November 2026** mit der offiziellen OpenCode- und IFM-Dokumentation abgeglichen. Sie verwenden das Konfigurationsformat von **OpenCode 2**. Downloadangebote, Oberflächen und API-Limits können sich ändern. Ein vollständiger Installationstest auf den drei Zielplattformen und ein Live-Test mit IFM-Zugangsdaten stehen noch aus.

## Struktur

```text
README.md                      Überblick und Einstieg
LICENSE                        Vollständiger CC-BY-4.0-Lizenztext
docs/                          Installation und Konfiguration
examples/opencode.ifm.json      Vorlage ohne API-Schlüssel
```

## Dokumentation pflegen

- Schreibe auf Deutsch und kennzeichne Meinungen, Vorschläge und beschlossene Entscheidungen eindeutig.
- Ergänze bei veränderlichen technischen Angaben eine Primärquelle und das Datum des Abgleichs.
- Prüfe bei Änderungen an der Konfiguration auch die zugehörige Anleitung.
- Speichere API-Schlüssel außerhalb des Repositorys. `.scratch/` ist für lokale Arbeitsnotizen vorgesehen und wird von Git ignoriert.

Änderungen lassen sich lokal mit `git status` und `git diff` prüfen und anschließend gezielt mit `git add` und `git commit` versionieren.

## Lizenz

Die Inhalte dieses Repositorys, einschließlich der Konfigurationsbeispiele, stehen unter **Creative Commons Namensnennung 4.0 International (CC BY 4.0)**, soweit nicht ausdrücklich anders gekennzeichnet.

Zur Namensnennung kann **„OSEG-AI-Mitwirkende“** verwendet werden. Verlinke bei einer Weitergabe die verwendete Originalfassung und die Lizenz; kennzeichne vorgenommene Änderungen. Ein möglicher Hinweis lautet:

> OSEG-AI-Mitwirkende, „OSEG-AI“, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Quelle: [oseg-ki-docs](https://github.com/AlexDorsten/oseg-ki-docs). Änderungen: Beschreibung der Änderungen.

Bei einer Weitergabe möglichst die verwendete Fassung verlinken und die Beschreibung der Änderungen anpassen. Der vollständige Lizenztext steht in [LICENSE](LICENSE); eine deutsche Erläuterung bietet [Creative Commons](https://creativecommons.org/licenses/by/4.0/deed.de). Verlinkte externe Projekte behalten ihre eigenen Lizenzen.
