---
title: iVS3D
subtitle: "Vorverarbeitung für Structure-From-Motion"
summary: Dieses Open-Source Projekt dient zum Vorverarbeiten von Bildsequenzen und Videos für die 3D-Rekonstruktion
date: 2025-12-22
cardimage: ivs3d_card.png
featureimage: ivs3d_card.png
caption: Hauptfenster von iVS3D mit ausgewählten Bildern und deren GPS Positionen.
level: university
authors:
  - Dominik: author.png
links:
  - github: https://github.com/iVS3D/iVS3D
---

## Intelligent Video Sampler 3D
iVS3D (Intelligent Video Sampler 3D) ist ein Open-Source-Framework zur Vorverarbeitung für die 3D-Rekonstruktion. Anstatt jedes einzelne Videoframe in eine Structure-from-Motion-Pipeline zu geben, hilft iVS3D dabei, einen saubereren und effizienteren Datensatz zu erzeugen: ausgewählte Bilder, synchronisierte Metadaten und optionale Segmentierungsmasken.

{{< vidSingle src="https://github.com/iVS3D/iVS3D/raw/refs/heads/master/iVS3D.mp4" poster="images/thumbnail.png" width="100%" >}}

In den letzten Jahren habe ich an diesem Projekt mit einem starken Fokus auf Engineering und Erweiterbarkeit mitgearbeitet. Ein wichtiger Teil meiner Arbeit waren Integration und Pflege plattformübergreifender Tools wie Qt, OpenCV und CMake, damit die Anwendung auf unterschiedlichen Betriebssystemen (Windows, Linux) und Hardwarekonfigurationen (mit/ohne CUDA) zuverlässig gebaut und eingesetzt werden kann.

Ein weiterer Schwerpunkt war die Entwicklung der Plugin-Architektur. Diese ermöglicht es, neue Algorithmen für Bildauswahl, Maskenerzeugung und Datenvisualisierung hinzuzufügen, wodurch Experimente und Forschungsiterationen deutlich schneller werden. Dadurch entwickelt sich iVS3D von einem reinen Frame-Sampler zu einem flexiblen Vorverarbeitungsframework für unterschiedliche Rekonstruktionsszenarien.

Ausserdem habe ich an der Integration neuronaler Netze mithilfe der ONNX Runtime gearbeitet, darunter semantische Segmentierung (ConvNeXt, BiseNet), Objekterkennung (YOLO) und Visual Similarity (ResNet). Dadurch können nützliche Frames identifiziert, störende Inhalte herausgefiltert und Masken erzeugt werden. Diese verbessern die Qualität der nachgelagerten Rekonstruktion.

{{< figSingle src="images/semseg.png" caption="iVS3D Semantic Segmentation." >}}

Einer der praktischsten Aspekte ist die direkte Brücke zur Rekonstruktion: iVS3D kann vorbereitete Daten exportieren und COLMAP/OpenMVS-Workflows lokal oder auf einem Remote-System starten. In Kombination mit sofort nutzbaren Releases (CPU- und CUDA-Builds) und einer erweiterbaren Plugin-Schnittstelle ist iVS3D eine solide Grundlage für Forschung und angewandte SfM-Projekte.