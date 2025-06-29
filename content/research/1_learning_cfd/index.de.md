---
title: Learning Surrogate Models for Fluid Dynamics
subtitle: "Seminararbeit am KIT"
summary: "Können physikalische Grundlagen von teuren Strömungssimulationen durch Neuronale Netze approximiert werden? Um diese Frage zu beantworten wird ein Literaturreview durchgeführt und verschiedene aktuelle Forschungsansätze verglichen. Grundlegende verwendete Architekturen wie CNNs, GNNs und LSTMs werden hergeleitet und deren Vor- und Nachteile anhand der Literatur diskutiert. Die Ergebnisse zeigen, dass Neuronale Netze in der Lage sind, Strömungssimulationen zu approximieren und dies in vielen Fällen schneller als traditionelle numerische Verfahren."
date: 2021-03-15
cardimage: learning_cfd_card.png
featureimage: learning_cfd.png
caption: "3D Strömungssimulation mit einem CNN ([Link zur Bildquelle](https://github.com/google/FluidNet))"
authors:
  - Dominik: author.png
links:
  - pdf: /files/Proseminar_Learning_Surrogate_Models_For_Fluid_Simulation.pdf
---

## Literaturübersicht
In dieser Seminararbeit habe ich eine Literaturübersicht (Literature Review) über Publikationen zu Ersatzmodellen für Fluiddynamik erstellt. Zunächst filterte ich nach Schlüsselwörtern wie "Fluiddynamik", "Ersatzmodell" und "Neuronales Netz".
Anschließend las ich die Abstracts der Arbeiten und wählte diejenigen aus, die für mein Thema relevant waren. Die ausgewählten Arbeiten wurden dann detailliert analysiert, wobei der Fokus auf den verwendeten Methoden, den erzielten Ergebnissen und den Grenzen der Ansätze lag. Es ist wichtig, die anfänglichen Schlüsselwörter so breit wie möglich zu halten, um sicherzustellen, dass alle relevanten Arbeiten in die Übersicht einbezogen werden. Daher habe ich auch Schlüsselwörter wie "Finite-Elemente-Methode" (FEM), "Large Eddy Simulation" (LES), "Partikelsimulation" und "Convolutional Neural Networks" (CNNs) einbezogen, um eine breite Palette von Ansätzen abzudecken. Wie unten gezeigt, ist die Anzahl der Publikationen zu diesem Thema in den letzten Jahren erheblich gestiegen.

{{< figSVG src="images/chart_n_publications.svg" caption="Publikationen pro Jahr über FEM, die neuronale Netze beinhalten." >}}

## Überblick und Vergleich der Ansätze
Die Literaturübersicht ergab, dass es viele verschiedene Ansätze für die Verwendung neuronaler Netze in der Fluiddynamik gibt. Einige Ansätze verwenden CNNs zur Approximation der Navier-Stokes-Gleichungen, während andere Graph Neural Networks nutzen, um die Wechselwirkungen zwischen Partikeln in einer Flüssigkeit zu modellieren. Manche Ansätze verwenden auch LSTMs zur Modellierung der zeitlichen Entwicklung der Fluiddynamik. Jeder Ansatz hat seine eigenen Vor- und Nachteile, die ich in der Arbeit zusammengefasst habe.

{{< figGIF src="images/canyon.gif" caption="Ein CNN wird verwendet, um eine partikelbasierte Fluidsimulation zu approximieren. ([Link zur Bildquelle](https://github.com/isl-org/DeepLagrangianFluids))" >}}

## Forschungsprozess
Da dies mein erstes wissenschaftliches Forschungsprojekt war, musste ich mich mit dem Forschungsprozess vertraut machen. Ich lernte, wie man eine Literaturübersicht erstellt, bestehende Arbeiten recherchiert und analysiert, wie man eine wissenschaftliche Arbeit schreibt und die Ergebnisse präsentiert. Als Teil des Seminars führten wir Peer-Review-Sitzungen durch, in denen wir die Arbeiten der anderen überprüften und Feedback gaben. Dies half mir, meine Schreibfähigkeiten zu verbessern und zu lernen, wie man konstruktives Feedback gibt. Ich lernte auch, wie man die Ergebnisse klar und prägnant präsentiert.

## Danksagung
Ich möchte meinem Betreuer, Dr. Till Riedel, für seine Unterstützung und Anleitung während des gesamten Forschungsprozesses danken. Besonderen Dank auch an meine Mitstudenten für ihr Feedback während der Peer-Review-Sitzungen. Ich habe viel aus dieser Erfahrung gelernt und bin dankbar für die Gelegenheit, diese Forschung durchführen zu können.