---
title: Realtime Rendering
subtitle: "Praktikum am KIT"
summary: In diesem Praktikum wurden auf Basis eines OpenGL frameworks verschiedene Techniken zur Bilderzeugung in Echtzeit implementiert. Diese beinhalten Level of Detail (LOD) Techniken, Precomputed Lighting, Path Guiding, Denoising und ReSTIR.
date: 2025-04-26
cardimage: realtime_rendering_card.png
featureimage: realtime_rendering_card.png
caption: Village-Szene gerendert mit ReSTIR.
authors:
  - Dominik: author.png
---

## Aufgabe 1: Level of Detail (LOD)
In der ersten Aufgabe habe ich eine Level-of-Detail (LOD) Technik für Terrain-Rendering implementiert. Dabei wird eine Heightmap zur Generierung eines Terrain-Meshes verwendet und ein Tessellations-Shader angewendet, der das Mesh adaptiv basierend auf der projizierten Bildschirmfläche jedes Quads verfeinert. Die Technik ermöglicht ein effizientes Rendering großer Landschaften bei gleichbleibender visueller Qualität. Es handelt sich um eine Implementierung des Concurrent Binary Tree (CBT)-Algorithmus, der die Detailstufe dynamisch in Abhängigkeit von Kameraposition und Blickrichtung anpasst. Wie in dem Paper [Concurrent Binary Trees (with application to longest edge bisection)](https://onrendering.com/data/papers/cbt/ConcurrentBinaryTrees.pdf) von Jonathan Dupuy (Unity Technologies) beschrieben, passt die Datenstruktur gut zu modernen GPU-Architekturen, was eine effiziente Traversierung und Darstellung des Terrain-Meshes ermöglicht.

{{< figSingle src="images/1_cbt_terrain.png" caption="CBT-Implementierung für adaptive Terrain-Tessellation. Das Mesh ist in Kameranähe fein aufgelöst. Weiter entfernt und außerhalb des Sichtfelds wird eine zunehmend gröbere Tessellation angewendet, ohne sichtbare Diskontinuitäten zu erzeugen. In dieser Debug-Ansicht sind die verschiedenen Baumebenen farbig visualisiert." >}}

## Aufgabe 2: Vorberechnete Beleuchtung
Basierend auf der Präsentation [Large-scale Global Illumination at Activision](https://research.activision.com/publications/2021/09/large-scale-global-illumination-in-call-of-duty) habe ich eine Technik zur Vorberechnung von globaler Beleuchtung unter Verwendung von Spherical Harmonics (SH) implementiert. Dabei wird ein vorab berechnetes, "Warped Irradiance-Volume" genutzt, um die Beleuchtungsinformationen für jeden Punkt einer Oberfläche zu speichern. Ein räumliches Gitter speichert die SH-Koeffizienten, welche interpoliert und zur Auswertung der indirekten Beleuchtung zur Laufzeit verwendet werden können. Diese Technik ermöglicht eine effiziente Darstellung komplexer Beleuchtung mit minimalem Laufzeitaufwand. Die vertikale Auflösung wird verbessert, indem die Höhe an die lokale Geometrie anstatt an die Gesamtszenenhöhe angepasst wird. Obwohl dies die trilineare Interpolation erschwert, führt es zu einer genaueren Repräsentation der Beleuchtung in der Szene. Während der Offline-Berechnung der SH-Koeffizienten werden die Licht-Samples validiert, sodass nur Beleuchtung durch äußere Bereiche einfließt – dies reduziert Abdunklungen und Lichtleck-Artefakte.

{{< figSingle src="images/2_precomputed.png" caption="Vorberechnete Beleuchtung mit Spherical Harmonics. Die Szene wird durch Umgebungslicht und eine gerichtete Lichtquelle beleuchtet. Beide tragen zur Gesamtbeleuchtung bei. Realistische Umgebungsbeleuchtung und dezentes Farbbluten sind unter den Bäumen zu erkennen." >}}

## Aufgabe 3: Path Guiding und Denoising
Die dritte Aufgabe befasste sich mit Path Guiding und Denoising-Techniken. Ich habe einen Path-Guiding-Algorithmus implementiert, der eine von Mises-Fisher-Verteilung in einem bildschirmgroßen Puffer speichert. Der Algorithmus basiert auf dem Paper [Real-Time Path-Guiding Based on Parametric Mixture Models](https://arxiv.org/abs/2112.09728) von Mikhail Derevyannykh. Über den Aufgabenrahmen hinaus habe ich eine temporale Reprojektion der per-Pixel-Verteilungen sowie räumlichen Sample-Reuse implementiert, um die Lerngeschwindigkeit des Algorithmus zu verbessern.

Selbst mit Guiding ist die Beleuchtung in komplexen Szenen mit vielen Lichtquellen oft verrauscht. Um dem entgegenzuwirken, habe ich einen Denoiser basierend auf dem Paper [Edge-Avoiding À-Trous Wavelet Transform for Fast Global Illumination Filtering](https://jo.dreggn.org/home/2010_atrous.pdf) von Dammertz et al. implementiert. Dieser nutzt eine Wavelet-Transformation, um das Rauschen zu filtern, ohne Kanten und Details zu verlieren. Die à-trous-Filterimplementierung erzielt eine hohe Performance auf der GPU. Eine Kombination aus drei Kantenstoppfunktionen basierend auf Farbwert, Oberflächennormalen und Weltkoordinaten wird verwendet, um hochfrequente Details wie scharfe Schatten oder Objektkanten zu erhalten.

{{< figSingle src="images/3_pg_denoising.png" caption="*Links*: Path-Tracing. *Mitte*: Nach Denoising. *Rechts*: Path-Guiding-Ergebnis nach wenigen Sekunden Lernen der Verteilungen." >}}

## Projekt: ReSTIR
Als Abschlussprojekt des Kurses hatten wir die Möglichkeit, ein beliebiges Verfahren zu implementieren. Gemeinsam mit Felix Mühlenberend habe ich am Reservoir-based SpatioTemporal Importance Resampling (ReSTIR) gearbeitet. Der Fokus liegt dabei auf effizientem Abtasten der direkten Beleuchtung in Szenen mit vielen Lichtquellen. Zunächst extrahierten wir die emittierende Geometrie beim Laden der Szene und integrierten Light-Sampling in das Framework. Danach implementierten wir [Resampled Importance Sampling (RIS)](https://diglib.eg.org/items/7b8d7c38-ee96-4415-acdd-3dd164fa8fad) gemäß der Beschreibung im Paper von Talbot et al. Schließlich erweiterten wir dies zu vollem ReSTIR, indem wir die spatio-temporalen Resampling-Schritte wie im [ReSTIR paper](https://research.nvidia.com/sites/default/files/pubs/2020-07_Spatiotemporal-reservoir-resampling/ReSTIR.pdf) von Bitterli et al. implementierten. Auf Empfehlung der Autoren ergänzten wir eine Alias-Tabelle, um die Sample-Generierung anhand der Flächeninhalte effizienter zu gestalten. Dies führte zu einem signifikanten Performanzgewinn gegenüber unserer naiven Sample-Generierung. Wir evaluierten unsere Implementierungen in verschiedenen Szenen und präsentierten die Ergebnisse unseren Kommilitonen.

{{< figSingle src="images/4_restir_result.png" caption="RIS und ReSTIR im Vergleich zu uniformem Licht-Sampling in einer komplexen Many-Light-Sponza-Szene." >}}

## Fazit
Der Kurs bot eine hervorragende Gelegenheit, verschiedene Verfahren des Echtzeit-Renderings zu implementieren und zu erproben. Die Aufgaben und das Projekt ermöglichten mir ein tieferes Verständnis der zugrunde liegenden Algorithmen und ihrer praktischen Anwendung in modernen Game Engines. Die Nutzung von OpenGL und GLSL für die Implementierung lieferte eine solide Grundlage für das Erlernen von Grafikprogrammierung und Echtzeit-Rendering-Techniken. Insgesamt war der Kurs eine wertvolle Erfahrung, die meine Kenntnisse im Bereich Computergrafik und Echtzeit-Rendering deutlich erweitert hat.

Ein besonderer Dank gilt den Betreuern Addis Dittebrandt, Mikhail Derevyannykh und Dmitrii Klepikov für ihre Unterstützung im Verlauf des Kurses. Ebenfalls danke an Felix für die großartige Zusammenarbeit am ReSTIR-Projekt. Der Kurs war eine sehr lehrreiche Erfahrung und ich freue mich darauf, das gewonnene Wissen in zukünftigen Projekten anzuwenden.

## Wo ist der Code?
Auch wenn ich den Code gerne teilen würde, ist er leider nicht öffentlich verfügbar. Der Kurs wurde am Karlsruher Institut für Technologie (KIT) durchgeführt, und das Framework ist Teil der Kursmaterialien. Da viel Arbeit in die Erstellung der Aufgaben und des Frameworks geflossen ist, möchte ich zukünftigen Teilnehmern die Erfahrung nicht durch eine Veröffentlichung meiner Lösungen vorwegnehmen. Wer sich für den Kurs interessiert, dem empfehle ich einen Blick auf die Website des [Lehrstuhls für Computergraphik am KIT](https://cg.ivd.kit.edu/index.php) für weitere Informationen zu Kursen und Projekten.