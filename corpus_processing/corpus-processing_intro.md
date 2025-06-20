(corpus-processing_intro)=
# Korpusverarbeitung. Von Strings zu Token

````{margin}
```{admonition} Fragen oder Feedback 
:class: frage-feedback

<a href="https://github.com/quadriga-dk/Text-Fallstudie-1/issues/new?assignees=&labels=question&projects=&template=frage.yml" class="external-link" target="_blank">
    Stellen Sie eine Frage
</a> <br>
<a href="https://github.com/quadriga-dk/Text-Fallstudie-1/issues/new?assignees=&labels=feedback&projects=&template=feedback.yml" class="external-link" target="_blank">
    Geben Sie uns Feedback
</a>

Mit Ihren Rückmeldungen können wir unser interaktives Lehrbuch gezielt an Ihre Bedürfnisse anpassen.

```
````
`````{margin}
````{admonition} Zitierhinweis
:class: citation-information
```{literalinclude} /CITATION.bib
:language: bibtex
```
Skorinkin, D., Sluyter-Gäthje, H. & Trilcke, P. (2024). _Quantitative Analyse der Medienwellen der Spanischen Grippe (1918/19). Eine Fallstudie._ https://doi.org/10.5281/zenodo.15682652

`````


```{admonition} Korpusverarbeitung mit Natural Language Processing
:class: lernziele

1. Die Grundkonzepte des Natural Language Processing können erklärt und die Funktionen von Tokenisierung und Lemmatisierung für die Textanalyse beschrieben werden.

2. Die notwendigen Schritte zur automatischen Annotation eines Texts können aufgezählt und Vorteile der Tokenisierung gegenüber einfacheren Methoden der Worttrennung genannt werden.
```

Für die Ausführung einer digitalen Analyse, in diesem Fall die Analyse von Worthäufigkeiten über Zeit, wird ein über die Zeit gestreutes Korpus benötigt, das im txt-Format (oder einem anderen, computerlesbaren Format) vorliegt. Wir haben gezeigt, wie ein aus PDF-Dateien bestehendes Zeitungskorpus (siehe Kapitel ["Korpusaufbau"](corpus-collection_intro)) mittels OCR verarbeitet werden kann (siehe Kapitel ["OCR — Vom Bild zum Text"](ocr_intro)), sodass das resultierende Korpus aus Textdateien (mit Dateiendung '.txt') besteht.

```{figure} ../assets/images/flow-chart_corpus-processing.jpeg
---
height:
name: Flussdiagramm der Fallstudie
---
Flussdiagramm der Fallstudie, das aktuelle Arbeitspaket ist hevorgehoben.
```

Die im Korpus enthaltenen Textdateien werden jetzt mit linguistischen Informationen angereichert. Zuerst wird konzeptionell in die Methoden der Anreicherung eingeführt (Tokenisierung und Lemmatisierung), dann wird kurz darauf eingegangen, welche Möglichkeiten es in Python für die Anreicherung gibt. Im nächsten Schritt wird gezeigt, wie mit Hilfe von spaCy das Zeitungskorpus annotiert werden kann. Zum Schluss wird ein Resümee gezogen.
