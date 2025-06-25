---
title: Real Time Neural Path Guiding
subtitle: "Bachelorarbeit"
summary: Eine neuartige, auf einem Neuronalen Netz basierende Path-Guiding Technik für echtzeit Path-Tracing. Ein kleines Neuronales Netz wird online trainiert um die eingehende Beleuchtung an Oberflächen in der Szene zu approximieren. Diese Informationen werden zum Path-Guiding der Strahlen in zukünftigen Bildern verwendet.
date: 2023-03-30
cardimage: bachelorthesis_card.png
featureimage: bachelorthesis.png
caption: Titelseite und ein Ausschnitt über Aktivierungsfunktionen des Neuronalen Netzes aus meiner Bachelorarbeit.
authors:
  - Dominik: author.png
links:
  - github: https://github.com/dom-wuest/NeuralPathGuiding
---

## Abstrakt
Da moderne Grafikkarten hardwarebeschleunigtes Raytracing unterstützen, haben wir die Möglichkeit, Path-Tracing zur Bilderzeugung in echtzeit einzusetzen. Aus Zeitgründen ist die Anzahl der Strahlen pro Pixel und Frame stark beschränkt. Dies führt zu einer hohen Varianz in der Monte-Carlo-Schätzung für die Radiative-Transfer-Gleichung. In dieser Arbeit werden moderne Techniken zur Reduzierung der Varianz für direkte und indirekte Beleuchtung diskutiert. Der Schwerpunkt liegt auf der Darstellung dynamischer Szenen in Echtzeit.

Wir schlagen eine neuartige Path-Guiding Technik vor, um die Varianz zu reduzieren, indem wir eine Schätzung der einfallenden Beleuchtung innerhalb der Szene lernen. Ein Multilayer-Perceptron wird verwendet, um den räumlichen Bereich der Szene zu unteteilen, und ein parametrisiertes Modell wird angepasst, um die Verteilung der Beleuchtung an einem Oberflächenpunkt anzunähern. Während des Renderns kann diese Verteilung verwendet werden, um die Strahlen in Richtungen mit starker einfallender Beleuchtung zu lenken. Als parametrisiertes Modell untersuchen wir die Verwendung von Mises-Fisher-Verteilungen und leiten eine Verlustfunktion her, um das Multilayer-Perceptron online zu trainieren. Wir evaluieren verschiedene Strategien zum Sammeln von Trainingsdaten und testen unseren Ansatz an statischen und dynamischen Szenen.

## Konzept
Im Jahr 2021 haben Müller et al. eine Radiance-Caching Technik vorgestellt, bei der ein kleines Multilayer-Perceptron die Radianz in echtzeit lernen kann. Um diese Arbeit zu sehen, klicken Sie [hier](https://research.nvidia.com/publication/2021-06_real-time-neural-radiance-caching-path-tracing). Die Implementierung des Neuronalen Netzes von Müller ist schnell genug, um das Netz in jedem Bild zu trainieren und auszuwerten. In meiner Abchlussarbeit verwende ich den selben Ansatz, allerdings lernt das Multilayer-Perceptron die richtungsabhängige Verteilung der einfallenden Beleuchtung an einer Oberfläche. Im Gegensatz zur gesamten, über die Hemisphere integrierten Beleuchtung, wie sie bei bei Müllers Arbeit gelernt wird, kann die richtungsabhägige Verteilung genutzt werden, um zukünftige Strahlen in vielversprechende Richtungen zu lenken. Im Verlauf von etwa 60 Bildern ist das Multilayer-Perceptron in der Lage, eine Annäherung der Beleuchtungsverteilung in einfachen Szenen zu lernen, und damit das Rauschen des Path-Tracers zu reduzieren.

{{< figSingle src="images/learning_cornell.png" caption="Ein Neuronales Netz lernt im laufe der Zeit die Richtun zur Lichtquelle. Diese Information wird verwendet, um das Rauschen des Path-Tracers zu reduzieren." >}}

## Grenzen und zukünftige Arbeit
Im aktuellen Zustand leidet die Implementierung unter numerischer Instabilität, welche zu Flackern führt und in einigen Fällen NaNs in den Berechnungen verursacht. Dies ist höchstwahrscheinlich auf die verrauschten Trainingsdaten zurückzuführen. Wie in meiner Abschlussarbeit gezeigt, konnten diese Probleme durch Änderungen an der Verlustfunktion reduziert werden. Es gibt jedoch Raum für Verbesserungen, sodass weitere Forschung erforderlich ist.

Die Verwendung einer einkeuligen von-Mises-Fisher-Verteilung reicht für die Darstellung komplexerer Beleuchtung nicht aus. Die Kombination mehrerer solcher vMF oder anderer Verteilungen könnte die Qualität der Approximation erheblich verbessern. Wie unten gezeigt, nähert sich der vMF bei Punkten, die von entgegengesetzten Lichtquellen beleuchtet werden, der einfallenden Strahlungsdichte nur schlecht an. Dies führt in diesen Bereichen zu einer verrauschten Ausgabe.

{{< figSingle src="images/vMF_limits.png" caption="Einfache vMF approximiert die einfallende Beleuchtung von zwei gegenüberliegenden Lichtquellen nur schlecht." >}}

## Würdigung

Die Codebasis für meine Arbeit wurde freundlicherweise von Egor Feklisov und Dmitrii Klepikov von der Moskauer Staatsuniversität zur Verfügung gestellt. Ihre Arbeit hat mich schnell auf meine Forschung vorbereitet und viele interessante Experimente ermöglicht.

Besonderer Dank geht an Mikhail Dereviannykh und Dr. Johannes Schudeiske, die mir diese großartige Gelegenheit gegeben und mich während meiner Recherche mit wertvollen Ratschlägen unterstützt haben!

Schauen Sie sich ihre Forschung unter (https://www.mishok43.com/home) und (https://jo.dreggn.org/home/) an!