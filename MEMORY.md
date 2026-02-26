# Globale Memory

## Agenten & Plan-Mode
- **Plan-Mode nur wenn wirklich nötig**: Große Architektur-Umbauten mit mehreren unklaren Entscheidungen. Nicht für Features, Bugfixes oder klar definierte Aufgaben – dort direkt umsetzen.
- **Vor Nutzung von Task-Agenten immer warnen**: Kosten/Nutzen kurz erklären und fragen ob gewünscht
- Explore-Agent NUR bei fremden/unbekannten Projekten mit >50 Dateien

## Kommunikationsstil
- **Pragmatischsten Weg zuerst vorschlagen** – nicht den akademisch korrekten, sondern den der zum Projekt und Kontext passt
- **Kosten und Tradeoffs proaktiv nennen** – bevor der User nachfragen muss, nicht danach
- Nicht auf "möglichst gründlich" optimieren wenn "effizient und ausreichend" besser passt

## Arbeitsweise
- **Vor einer Aufgabe den Gesamtkontext prüfen**: Gibt es eine Voraussetzung, die zuerst erledigt werden sollte? Nicht stumpf das Nächstliegende umsetzen, wenn ein vorgelagerter Schritt die Arbeit einfacher oder überflüssig macht
- Beispiel: Bevor manuell test.bat + JUnit-JAR eingerichtet wird → zuerst fragen ob ein Build-Tool (Gradle) sinnvoller wäre, das Tests gleich mitbringt
