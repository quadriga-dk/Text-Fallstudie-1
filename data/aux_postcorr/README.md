# Hilfsdaten: LLM-Nachkorrektur

Dieser Ordner enthält zwei Zeitungsseiten, die zusätzlich zur regulären OCR
über die GPT-4-API nachkorrigiert wurden (Dateien mit dem Suffix
`_llm_postcorr`), jeweils als Text- und als Annotationsdatei.

Sie dienen ausschließlich der Demonstration im Kapitel
[Ausblick: Die Auswirkung der LLM-Nachkorrektur](../../reflection/reflection_LLM-post-correction.ipynb),
in dem die Anzahl der Grippe-bezogenen Wörter vor und nach der Nachkorrektur
verglichen wird.

**Sie gehören nicht zum Analysekorpus.** Es handelt sich um nachkorrigierte
Dubletten von Seiten, die bereits in `../txt` bzw. `../csv` enthalten sind, und
sie sind nicht in der Metadatentabelle
`../metadata/QUADRIGA_FS-Text-01_Data01_Corpus-Table.csv` verzeichnet. Lägen sie
in `../csv`, würden sie beim Einlesen des Korpus mitgezählt und in der
KWIC-Suche zu doppelten Treffern ohne Datumsangabe führen.
