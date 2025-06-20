(intro)=
# Quantitative Analyse der Medienwellen der Spanischen Grippe (1918/19). Eine Fallstudie

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


```{figure} ../assets/images/grippeocr.gif
---
height: 200px
name: Zeitungssnippet mit simuliertem OCR-Overlay
---
```

Die vorliegende Fallstudie bereitet – in Form eines ["Jupyter Books"](introduction_requirements) – den Prozess und die Ergebnisse eines Forschungsprojekts aus den Digital Humanities didaktisch auf. Schritt für Schritt wird nachvollziehbar, 

- wie eine **Forschungsfrage** entwickelt und operationalisiert wird, 
- ein entsprechendes **Korpus** aufgebaut, bereinigt und angereichert wird,
- um schließlich quantitative **Analysen** auf diesem Korpus durchzuführen.

Anhand von historischen Tageszeitungen wird dabei eine Frage aus dem Feld der Digital History nachgegangen: **Welchen quantitativen Mustern folgte die Berichterstattung über die Spanische Grippe in den Jahren 1918/1919?**

### Zielgruppe
Die Fallstudie richtet sich an Geisteswissenschaftler:innen auf fortgeschrittener Qualifikationsstufe. Kenntnisse der Digital Humnanites sind nicht erforderlich, wohl aber eine prinzipiell Neugier und Offenheit gegenüber digitalen Arbeitsweisen und quantifizierten Forschungsansätzen. 

 
### Struktur der Fallstudie
Die Gliederung der Fallstudie lässt sich jederzeit durch die Menüleiste links im Browser nachvollziehen. Insgesamt vollzieht die Fallstudie 6 Schritte: 

```{figure} ../assets/images/flow-chart.gif
---
height:
name: Flussdiagramm der Fallstudie
---
Flussdiagramm der Fallstudie, die sich aus sechs Arbeitspaketen zusammensetzt.
```

- Im **1. Schritt** entwickeln wir eine Forschungsfrage und operationalisieren diese Forschungsfrage für die quantitative Analyse, entwickeln also ein Konzept, wie wir mittels Meßoperationen zu einer Antwort auf die Forschungsfrage kommen (siehe Kapitel ["Fragestellung und Operationalisierung"](research-question_intro)).
- Im **2. Schritt** bauen wir ein Korpus aus Textobjekten für die Analyse auf, das zunächst aus PDF-Dateien besteht (siehe Kapitel ["Korpusaufbau"](corpus-collection_intro))
- Im **3. Schritt** machen wir die Textobjekte im Korpus, die zunächst nur als Bilddateien vorliegen, mittels Optical Character Recognition (OCR) maschinenlesbar (siehe Kapitel ["OCR — Vom Bild zum Text"](ocr_intro))
- Im **4. Schritt** evaluieren wir die OCR-Ergebnisse und testen Optionen zur Nachkorrektur (siehe Kapitel ["Nachkorrektur der OCR-Ergebnisse"](post-correcting_intro)).
- Im **5. Schritt** reichern wir mithilfe von Verfahren des Natural Language Processing (NLP) die Textobjekte im Korpus mit linguistischen Informationen an. (siehe Kapitel ["Korpusverarbeitung – Von Strings zu Token"](corpus-processing_intro)).
- Im **6. Schritt** führen wir die quantitativen Analysen auf dem Korpus durch und visualisieren die Ergebnisse (siehe Kapitel ["Korpusanalyse"](corpus-analysis_intro)).

Die Fallstudie schließt mit einer Reflexion und einem Ausblick (siehe Kapitel ["Reflexion und Resümee"](reflection_reflection)) 	
