---
title: PC Modding
subtitle: "Handgefertigte Kabel und Hardline-Wasserkühlung"
summary: In den letzten 6 Jahren habe ich meinen PC nach meinen Vorstellungen angepasst. Dazu gehören handgefertigte, individuell ummantelte Kabel, welche präzise verlegt wurden, sowie eine Hardline-Wasserkühlung für die CPU. Außerdem wird die RGB-Beleuchtung von einem ESP32-Mikrocontroller gesteuert.
date: 2022-01-10
cardimage: modding_card.jpeg
authors:
  - Dominik: author.png
---
## Mein PC
- Nvidia GeForce RTX 3070
- Amd Ryzen 5 7600X
- 32GB DDR5 RAM


## Individuell ummantelte Kabel

Mein PC-Gehäuse, das Phanteks Enthoo Evolv, verfügt auf beiden Seiten über gehärtete Glasscheiben. Das bedeutet, dass es keinen Platz zum Verstecken von Kabeln gibt und mein PC ohne ordentliches Kabelmanagement sehr chaotisch aussah. Um dies zu beheben, habe ich ein modulares Netzteil von Corsair gekauft und meinen eigenen Kabelsatz erstellt. Jeder Draht wurde einzeln auf Länge geschnitten und mithilfe spezieller Halterungen aus Aluminium verlegt. Auf diese Weise sind keine Drähte lose und es bleiben keine Kabel übrig, die irgendwo verstaut werden müssen. Beide Enden wurden gecrimpt und mit ATX/Molex-Anschlüssen verbunden.

Um das Aussehen noch weiter zu verbessern, wurde jedes Kabel entweder in Rot oder Karbongrau ummantelt, passend zum Farbthema der Hardware.

{{< figGrid subfolder="images" figCaption="Oben: Benötigte Werkzeuge zum Schneiden von Drähten, Crimpen und Hülsen. Und das Endergebnis. Unten: Wasserkühlung und Beleuchtung im Betrieb." >}}

## Hardline-Wasserkühlung

Als PC Enthusiast war es schon einige Jahre mien Traum, eine Wasserkühlung in meinen PC einzubauen. Während der Corona-Pandemie konnte ich mir dann endlich die nötigen Komponenten leisten. Ich habe mich für einen CPU-Kühlblock von Phanteks, sowie einen Radiator und eine Pumpe von Singularity Computers entschieden. Diese drei Komponenten habe ich mit Acryl-Rohren von Alphacool verbunden. Dazu wurden die Rohre erhitzt, von Hand an den passenden Stellen gebogen und auf die richtige länge gekürzt. Auf diesem Weg wird die Kühlflüssigkeit von der Pumpe zum CPU-Wasserblock transportiert, dort absorbiert es die Abwärme der CPU. Anschließend fließt ddie Kühlflüssigkeit durch den Radiator, welcher im Deckel verbaut ist. Dort wird die Wärme an die Umgebungsluft abgegeben. Der Kühlkreislauf ist dann zur Pumpe hin geschlossen. Die Installation der Komponenten hat einige Stunden gedauert, insbesondere das Biegen und zurechtschneiden der Acryl-Rohre war aufwändig. Nachdem ich den Kühlkreislauf auf undichte Stellen geprüft (und dabei ein Leck an der Pumpe abgedichtet) habe, ist die Wasserkühlung nun mit blutroter Flüssigkeit in Betrieb.

## RGB-Beleuchtung mit einem ESP32-Microcontroller

Um die handgefertigten Kabel und die Wasserkühlung perfekt in Szene zu setzen, habe ich RGB Beleuchtungen verbaut. Da das Innere des Gehäuses sowie die PC Komponenten überwiegend in Schwarz gehalten sind, wird viel Licht absorbiert und es sind dahre viele LEDs nötig. Am Radiator im Deckel habe ich daher drei RGB Lüfter von Corsair installiert. Dadurch werden Mainboard und Grafikkarte gleichmäßg beleuchtet. Im unteren Gehäuseteil habe ich ebenfalls einen LED Streifen angebracht. Da mein Arbeitsspeicher nicht mit RGB Beleuchtung ausgestattet war, habe ich DIY Heatsinks für diesen gekauft. Somit hat nun auch mein Arbeitsspeicher LED Beleuchtung.

Um die ganzen RGB LEDs zu synchronisieren habe ich einen ESP32 Microcontroller verwendet. Dieser ist im Deckel verbaut und über die interne USB Schnittstelle mitr dem Mainboard verbunden. Der Microcontroller steuert die Beleuchtung der Lüfter, Arbeitsspeicher und LED-Streifen. Über die USB Verbindung kann mithilfe eine C# Desktopanwendung zwischen verschiedenen Animationen und Farben gewechselt werden.