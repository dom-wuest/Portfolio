---
title: Ambilight
subtitle: "Dynamische Hintergrundbeleuchtung mit Arduino"
summary: Dieses Projekt implementiert eine dynamische Ambilight-Lösung für Bildschirme. Dabei wird ein Arduino verwendet, um die LED-Streifen basierend auf dem Bildinhalt zu steuern. Auf dem Desktop wird die Bildschirmaufnahme verwendet, um die Farben am Bildschirmrand zu erfassen und an die LED-Streifen zu übertragen.
date: 2018-01-18
cardimage: ambilight_card.jpg
featureimage: ambilight_card.jpg
caption: Beispiel für eine Ambilight-Installation mit LED-Streifen.
level: school
keywords:
  - Arduino
  - LED-Steuerung
  - C++ / C#
authors:
  - Dominik: author.png
---

## Ambilight
Fernseher und Computerbildschirme sind in ihrer Größe begrenzt, und in den meisten Fällen erstreckt sich die menschliche visuelle Wahrnehmung über die physischen Grenzen des Displays hinaus. Um das Seherlebnis zu verbessern, schafft Ambilight eine immersivere Umgebung, indem es die Farben vom Bildschirm auf die umliegenden Wände projiziert. Diese Technologie ist von Philips patentiert und daher nicht offen für die Nutzung in anderen Produkten verfügbar. Mit ein paar adressierbaren RGB-LED-Streifen und einem Arduino kann jedoch ein ähnlicher Effekt erzielt werden.

### Farberfassung

Für dieses System müssen die Farben an den Bildschirmrändern erfasst und an die LED-Streifen gesendet werden. Idealerweise würde man die Bilddaten direkt vom Videosignal erfassen. Dazu müsste man den Video-Stream decodieren, was in modernen Systemen HDMI oder DP wäre und somit den Rahmen eines Spielzeugprojekts sprengt. Stattdessen haben wir eine Desktop-Anwendung implementiert, um den Bildschirminhalt zu erfassen und die relevanten Farbinformationen zu extrahieren.

### Beleuchtung der LED-Streifen
Sobald die Farbinformationen extrahiert sind, müssen sie an die LED-Streifen gesendet werden. Dies geschieht über den Arduino, der die Farbdaten über USB empfängt und die LED-Streifen entsprechend steuert. Da der Arduino dedizierte USART-Hardware für die serielle Kommunikation hat, kann er den Datentransfer effizient handhaben, ohne das Hauptprogramm zu blockieren. Außerdem gibt es Bibliotheken, welche die Steuerung von LED-Streifen vereinfachen, wie die NeoPixel-Bibliothek von Adafruit. Der Arduino-Code wartet auf eingehende Daten und aktualisiert die LED-Farben in Echtzeit, wodurch ein nahtloser Ambient-Lichteffekt entsteht, der mit dem Bildschirminhalt übereinstimmt.

### Konfiguration
Um verschiedene Bildschirmgrößen zu unterstützen, ermöglicht die Desktop-Anwendung den Benutzern, die Anzahl der LEDs und deren Positionen relativ zum Bildschirm in einer GUI zu konfigurieren. Die Anwendung berechnet dann die entsprechende Farbzuordnung und sendet die Konfigurationsdaten zur Verarbeitung an den Arduino. Zusätzliche Einstellungen, wie die Wahl der Anordnung der LED-Streifen im Uhrzeigersinn oder gegen den Uhrzeigersinn oder das Vermeiden von schwarzen Balken bei 21:9-Inhalten, können ebenfalls angepasst werden.

{{< figSingle src="images/1_ui.png" caption="Hauptanwendungsfenster von Ambilight mit der Konfiguration der LED-Streifen." >}}

### Funktionen
- Echtzeit-Farberfassung vom Bildschirm
- USB-Kommunikation mit Arduino zur LED-Steuerung
- Konfigurierbare LED-Streifen-Anordnung und -Einstellungen
- Unterstützung für verschiedene Bildschirmgrößen und -formaten
- Unterstützung für 21:9-Inhalte mit schwarzen Balken
- Wählbare Farbprofile für verschiedene Lichtumgebungen
- Wählbarer COM-Port für die Arduino-Verbindung

### Einschränkungen
- Das System ist auf die Bildschirmaufnahme angewiesen, was zu Latenz oder Ungenauigkeiten bei der Farbdarstellung führen kann.
- Die begrenzte Baudrate der seriellen Schnittstelle des Arduino führt zu niedrigen Bildwiederholraten.
- Es ist eine Desktop-Anwendung erforderlich, um den Bildschirminhalt zu erfassen, sodass es nicht auf Fernsehern oder Konsolen funktioniert.