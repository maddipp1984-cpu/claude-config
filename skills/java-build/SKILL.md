---
name: java-build
description: Builds a Java project without Maven/Gradle. Use when the user says "java-build", "build", "kompilieren", "JAR bauen", "release bauen" or wants to compile and package a Java desktop application with javac and jar.
disable-model-invocation: true
---

# Java Build Skill

Baue das aktuelle Java-Projekt (kein Maven/Gradle). Argumente: `$ARGUMENTS`

## Schritt 1 – Projekt analysieren

Lies zuerst die CLAUDE.md des Projekts (falls vorhanden), dann prüfe:
- Gibt es eine `build.bat`? Wenn ja: lies sie und führe sie mit Bash aus. Fertig.
- Wenn nicht: weiter mit Schritt 2.

## Schritt 2 – Build-Parameter ermitteln

Suche per Glob nach:
- `src/**/*.java` → Quellcode-Wurzel
- `lib/*.jar` → externe JARs (Classpath)
- `*.md` → CLAUDE.md oder README für Ausgabepfad und Hauptklasse

Ermittle:
- **JDK-Pfad**: `C:\Users\maddi\.jdks\openjdk-25.0.2` (aus globalem CLAUDE.md)
- **Hauptklasse**: Suche per Grep nach `public static void main` in den Java-Dateien
- **Paketname**: aus der `package`-Deklaration der Hauptklasse
- **JAR-Name**: Projektverzeichnisname oder CLAUDE.md-Projekttitel
- **Ausgabeverzeichnis**: `bin/` für Klassen, `dist/` oder `release/` für JAR/EXE

## Schritt 3 – Kompilieren

```bat
SET JDK=C:\Users\maddi\.jdks\openjdk-25.0.2
SET SRC_FILES=... (alle .java rekursiv)
SET CLASSPATH=lib\ojdbc11.jar;lib\...

%JDK%\bin\javac -encoding UTF-8 -cp %CLASSPATH% -d bin %SRC_FILES%
```

Gib Compiler-Fehler vollständig aus. Bei Fehlern: stoppe und erkläre das Problem.

## Schritt 4 – Fat-JAR bauen

```bat
REM Manifest erstellen
echo Main-Class: com.example.MainClass > manifest.txt
echo Class-Path: . >> manifest.txt

REM Klassen + externe JARs extrahieren und neu packen
cd bin
%JDK%\bin\jar xf ..\lib\dependency.jar
cd ..
%JDK%\bin\jar cfm dist\AppName.jar manifest.txt -C bin .
```

## Schritt 5 – jpackage (optional, nur wenn EXE gewünscht)

Nur ausführen, wenn der Nutzer eine `.exe` / installierbare App möchte oder die build.bat jpackage enthält:

```bat
%JDK%\bin\jpackage ^
  --type app-image ^
  --input dist ^
  --main-jar AppName.jar ^
  --main-class com.example.MainClass ^
  --name AppName ^
  --dest release
```

## Schritt 6 – Ergebnis melden

Melde kurz:
- Kompilierungsstatus (Anzahl Klassen)
- Pfad zur JAR-Datei
- Pfad zur EXE (falls erzeugt)
- Etwaige Warnungen

## Wichtige Hinweise

- **Immer UTF-8**: `javac -encoding UTF-8`
- **Classpath-Separator**: Windows = `;`, Unix = `:`
- **Bash-Shell in VS Code**: Pfade mit `/c/Users/...` oder mit `cmd /c build.bat` über Bash aufrufen
- Falls build.bat vorhanden: immer bevorzugen, nicht neu erfinden
- Bei fehlendem JDK-Pfad: aus CLAUDE.md lesen oder Nutzer fragen
