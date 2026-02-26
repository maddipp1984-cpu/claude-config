# Globale Einstellungen

## Sprache
- Kommunikation auf Deutsch

## Modell & Workflow
- Standard: `claude-sonnet-4-6` (Sonnet 4.6) – für Entwicklung und Umsetzung
- Nach Abschluss eines Features/Tools: `/model claude-opus-4-6` für Code-Review (Logikfehler, Randfälle, konzeptionelle Probleme)
- Opus nur für Reviews und komplexe Logik-Analyse, nicht für reine Umsetzung

## Entwicklungsumgebung
- Windows 11
- VS Code
- Java 11 (Arbeitsrechner), JDK-Pfad: `C:\Users\maddi\.jdks\openjdk-25.0.2` (Entwicklungsrechner)
- Kein Python installiert
- 7-Zip verfügbar: "C:\Program Files\7-Zip\7z.exe"
- PowerShell: Skriptausführung aktiv

## Token-Sparsamkeit
- Bei Sessionbeginn zuerst CLAUDE.md und Memory lesen – wenn das Projekt dort dokumentiert ist, reicht das als Kontext
- Nur Dateien per Read laden, die tatsächlich editiert werden sollen
- Bei eigenen/gemeinsam erstellten Projekten: NIEMALS das Projekt neu analysieren, die Doku ist aktuell

## Dokumentation
- Nach Abschluss eines Features die Projekt-CLAUDE.md aktualisieren (Struktur, Designentscheidungen, Persistenz-Dateien)
- `TODO.md` im Projektroot für geplante Features/nächste Schritte – am Sessionstart mit lesen
- Erledigte Einträge in TODO.md nach Abschluss abhaken oder entfernen

## Sessionstart
- Globale `TODO.md` lesen (`C:\Users\maddi\.claude\TODO.md`) und fragen: „Möchtest du offene TODOs bearbeiten?"
- Projekt-`TODO.md` (falls vorhanden) ebenfalls lesen und separat fragen

## Dateisystem
- NIEMALS OneDrive für Projektdaten oder Ablage nutzen
- Einzige Ausnahme: Desktop-Pfad ist `C:\Users\maddi\OneDrive\Desktop\` (OneDrive-Umleitung aktiv)

## Java-Projekt-Template (Gradle)
- **Wenn ein leeres/neues Projektverzeichnis erkannt wird**: proaktiv anbieten, das Gradle-Template aufzusetzen (build.gradle, Wrapper, src/test-Struktur, CLAUDE.md, TODO.md)
- Nur Projektname und GUI vs. CLI erfragen, Rest automatisch anlegen

Bei neuen Java-Projekten: Gradle mit Wrapper, Shadow-Plugin für Fat-JAR, jlink für minimale JRE.
- `build.gradle`: java + application + shadow Plugin, sourceCompatibility '11', UTF-8 Encoding
- `settings.gradle`: rootProject.name
- Source-Layout: `src/` (main), `test/` (JUnit 5)
- Oracle JDBC als lokales JAR in `lib/` (nicht in Maven Central)
- Wrapper generieren: einmalig `gradle wrapper` mit installiertem Gradle, danach nur noch `./gradlew`
- Referenzprojekt: MergeGen (`C:\projekte\mergegen\build.gradle`)

## Was wohin gehört
- **Globale CLAUDE.md** (diese Datei): Feste Regeln, Umgebung, Workflow, Fakten
- **Projekt-CLAUDE.md**: Architektur, Struktur, Designentscheidungen, Build-Infos
- **Globale MEMORY.md**: Gelerntes Verhalten – wie ich kommunizieren und arbeiten soll
- **Projekt-MEMORY.md**: Nur für projektspezifische Erfahrungen die NICHT in die Projekt-CLAUDE.md passen (selten nötig)
