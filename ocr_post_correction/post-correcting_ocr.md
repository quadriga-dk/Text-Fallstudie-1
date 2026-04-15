# Einführung in die OCR-Nachbearbeitung

Während OCR-Software heutzutage sehr leistungsfähig ist, sind die Ergebnisse nicht immer perfekt und erfordern häufig eine Nachbearbeitung, um Fehler zu korrigieren und die Textqualität zu verbessern.

Die Nachbearbeitung umfasst verschiedene Schritte, die sicherstellen, dass der umgewandelte Text korrekt und lesbar ist. Diese Schritte können manuell oder automatisiert durchgeführt werden und umfassen unter anderem die Korrektur von Tippfehlern, die Formatierung des Textes und die Überprüfung auf Vollständigkeit und Genauigkeit.

### Grundlegende Beispiele für die OCR-Nachbearbeitung

#### 1. Korrektur von Erkennungsfehlern

OCR-Software kann Buchstaben oder Wörter falsch erkennen, insbesondere wenn die Qualität des Originaldokuments schlecht ist. Häufige Fehler sind die Verwechslung von ähnlichen Buchstaben wie „l“ (kleines L) und „1“ (Eins), „O“ (großes O) und „0“ (Null) oder „rn“ (r und n) als „m“.

**Original (nach OCR):**
```
Der heutige Wert beläuft sich auf 1000€. 
Das wird ein lntensives Jahr.
```

**Nachbearbeitet:**
```
Der heutige Wert beläuft sich auf 1000€. 
Das wird ein intensives Jahr.
```

#### 2. Korrektur von Tippfehlern und Grammatik

Selbst wenn die OCR-Erkennung korrekt ist, können Tipp- und Grammatikfehler aus dem Originaldokument übernommen werden. Hier ist eine gründliche Überprüfung erforderlich.

**Original (nach OCR):**
```
Die Vereinbarung wurde am 15. März 2023 unterschireben.
```

**Nachbearbeitet:**
```
Die Vereinbarung wurde am 15. März 2023 unterschrieben.
```

#### 3. Wiederherstellung der Formatierung

OCR kann die Formatierung von Texten, wie z.B. Absätze, Überschriften, und Aufzählungen, nicht immer richtig interpretieren. Eine manuelle Nachbearbeitung ist oft notwendig, um die ursprüngliche Struktur des Dokuments wiederherzustellen.

**Original (nach OCR):**
```
Kapitel 1: Einleitung
Dieser Text behandelt das Thema OCR. 
- Punkt 1
- Punkt 2
Kapitel 2: Methodik
Die Methode basiert auf...
```

**Nachbearbeitet:**
```
Kapitel 1: Einleitung

Dieser Text behandelt das Thema OCR.

- Punkt 1
- Punkt 2

Kapitel 2: Methodik

Die Methode basiert auf...
```

#### 4. Überprüfung auf Vollständigkeit

Manchmal fehlen nach der OCR-Erkennung Teile des Textes, insbesondere wenn das Originaldokument beschädigt ist oder schlecht gescannt wurde. 

**Original (nach OCR):**
```
Die Forschungsergebnisse zeigen, dass...
Zur weiteren Überprüfung...
```

**Nachbearbeitet:**
```
Die Forschungsergebnisse zeigen, dass die Effizienz der neuen Methode signifikant höher ist.
Zur weiteren Überprüfung der Ergebnisse wurde eine zweite Studie durchgeführt.
```

### 🚀 Your turn: Interaktives Beispiel

Now that you have an understanding of the various OCR post-processing methods, you can try out the interactive exercises below!<br>

In this interactive element, you can use the check boxes to see how the post-processing steps explained above work in practice. Once a certain category is selected, the corresponding corrections will be highlighted in the text. Feel free to try with different combinations to see how the entire workflow comes together!</p>

<div style="border: 1px solid #ddd; padding: 15px; border-radius: 8px; margin-bottom: 20px;">
  <div style="margin-bottom: 15px; font-family: sans-serif;">
    <strong>Nachbearbeitungs-Schritte aktivieren:</strong><br><br>
    <label style="cursor: pointer; margin-right: 15px;">
      <input type="checkbox" id="chk-recog" onchange="updateOcrText()"> 1. Erkennungsfehler (l/i)
    </label><br>
    <label style="cursor: pointer; margin-right: 15px;">
      <input type="checkbox" id="chk-typo" onchange="updateOcrText()"> 2. Tippfehler (Dreher)
    </label><br>
    <label style="cursor: pointer; margin-right: 15px;">
      <input type="checkbox" id="chk-format" onchange="updateOcrText()"> 3. Formatierung (Absätze)
    </label><br>
    <label style="cursor: pointer;">
      <input type="checkbox" id="chk-comp" onchange="updateOcrText()"> 4. Vollständigkeit (Lücken)
    </label>
  </div>

  <div id="ocr-box" style="background-color: #f8f9fa; border: 1px solid #ced4da; padding: 15px; border-radius: 5px; font-family: monospace; white-space: pre-wrap; line-height: 1.5; color: #333;">
    </div>
</div>

<script>
  function updateOcrText() {
    const recog = document.getElementById('chk-recog').checked;
    const typo = document.getElementById('chk-typo').checked;
    const format = document.getElementById('chk-format').checked;
    const comp = document.getElementById('chk-comp').checked;

    // Highlight colors for corrected elements
    const styleRecog = recog ? 'background-color: #d4edda; font-weight: bold;' : '';
    const styleTypo = typo ? 'background-color: #fff3cd; font-weight: bold;' : '';
    const styleComp = comp ? 'background-color: #cce5ff; font-weight: bold;' : '';
    
    // Linebreaks change based on formatting toggle
    const lb = format ? '\n\n' : '\n'; 

    let html = '';
    
    html += format ? '<span style="background-color: #f8d7da; font-weight: bold;">Kapitel 1: Einleitung</span>' + lb : 'Kapitel 1: Einleitung\n';
    
    html += 'Dieser Text behandelt das Thema OCR. Der heutige Wert beläuft sich auf 1000€. Das wird ein ';
    html += recog ? `<span style="${styleRecog}">intensives</span>` : 'lntensives';
    html += ' Jahr. Die Vereinbarung wurde am 15. März 2023 ';
    html += typo ? `<span style="${styleTypo}">unterschrieben</span>` : 'unterschireben';
    html += '. Die Forschungsergebnisse zeigen, dass';
    html += comp ? `<span style="${styleComp}"> die Effizienz der neuen Methode signifikant höher ist.</span>` : '...';
    
    html += format ? '\n\n<span style="background-color: #f8d7da; font-weight: bold;">- Punkt 1\n- Punkt 2</span>\n\n' : '\n- Punkt 1\n- Punkt 2\n';
    
    html += format ? '<span style="background-color: #f8d7da; font-weight: bold;">Kapitel 2: Methodik</span>' + lb : 'Kapitel 2: Methodik\n';
    
    html += 'Die Methode basiert auf... Zur weiteren Überprüfung';
    html += comp ? `<span style="${styleComp}"> der Ergebnisse wurde eine zweite Studie durchgeführt.</span>` : '...';

    document.getElementById('ocr-box').innerHTML = html;
  }
  
  // Initialize the text box on page load
  updateOcrText();
</script>
<br>

In this second interactive widget, your goal is to match each text snippet with its correct post-processing category. Read the small blocks of text and try to select the category you think fits best. If your guess is correct, the text will turn green and reveal the correction; if incorrect, you will be prompted to try again.</p>

<p>Wählen Sie für jeden Textausschnitt die passende Nachbearbeitungs-Kategorie aus. Bei richtiger Auswahl wird der Text automatisch korrigiert.</p>

<div style="display: flex; flex-direction: column; gap: 15px; font-family: sans-serif;">

  <div id="card-1" style="border: 1px solid #ccc; padding: 15px; border-radius: 5px;">
    <div style="margin-bottom: 10px; font-family: monospace; font-size: 1.1em;" id="text-1">Das wird ein lntensives Jahr.</div>
    <select id="select-1" onchange="checkAnswer(1, 'recog')" style="padding: 5px;">
      <option value="">Fehlertyp auswählen...</option>
      <option value="recog">1. Erkennungsfehler (z.B. l statt i)</option>
      <option value="typo">2. Tippfehler und Grammatik</option>
      <option value="format">3. Wiederherstellung der Formatierung</option>
      <option value="comp">4. Überprüfung auf Vollständigkeit</option>
    </select>
    <span id="feedback-1" style="margin-left: 10px; font-weight: bold;"></span>
  </div>

  <div id="card-2" style="border: 1px solid #ccc; padding: 15px; border-radius: 5px;">
    <div style="margin-bottom: 10px; font-family: monospace; font-size: 1.1em;" id="text-2">Die Vereinbarung wurde am 15. März 2023 unterschireben.</div>
    <select id="select-2" onchange="checkAnswer(2, 'typo')" style="padding: 5px;">
      <option value="">Fehlertyp auswählen...</option>
      <option value="recog">1. Erkennungsfehler (z.B. l statt i)</option>
      <option value="typo">2. Tippfehler und Grammatik</option>
      <option value="format">3. Wiederherstellung der Formatierung</option>
      <option value="comp">4. Überprüfung auf Vollständigkeit</option>
    </select>
    <span id="feedback-2" style="margin-left: 10px; font-weight: bold;"></span>
  </div>

  <div id="card-3" style="border: 1px solid #ccc; padding: 15px; border-radius: 5px;">
    <div style="margin-bottom: 10px; font-family: monospace; font-size: 1.1em; white-space: pre-wrap;" id="text-3">Kapitel 1: Einleitung
Dieser Text behandelt das Thema OCR. 
- Punkt 1
- Punkt 2</div>
    <select id="select-3" onchange="checkAnswer(3, 'format')" style="padding: 5px;">
      <option value="">Fehlertyp auswählen...</option>
      <option value="recog">1. Erkennungsfehler (z.B. l statt i)</option>
      <option value="typo">2. Tippfehler und Grammatik</option>
      <option value="format">3. Wiederherstellung der Formatierung</option>
      <option value="comp">4. Überprüfung auf Vollständigkeit</option>
    </select>
    <span id="feedback-3" style="margin-left: 10px; font-weight: bold;"></span>
  </div>

  <div id="card-4" style="border: 1px solid #ccc; padding: 15px; border-radius: 5px;">
    <div style="margin-bottom: 10px; font-family: monospace; font-size: 1.1em;" id="text-4">Die Forschungsergebnisse zeigen, dass...</div>
    <select id="select-4" onchange="checkAnswer(4, 'comp')" style="padding: 5px;">
      <option value="">Fehlertyp auswählen...</option>
      <option value="recog">1. Erkennungsfehler (z.B. l statt i)</option>
      <option value="typo">2. Tippfehler und Grammatik</option>
      <option value="format">3. Wiederherstellung der Formatierung</option>
      <option value="comp">4. Überprüfung auf Vollständigkeit</option>
    </select>
    <span id="feedback-4" style="margin-left: 10px; font-weight: bold;"></span>
  </div>

  <button onclick="resetGame()" style="padding:6px 14px;background:#333;color:white;border:none;border-radius:4px;">Zurücksetzen</button>

</div>

<script>
  const originalTexts = {
    1: 'Das wird ein lntensives Jahr.',
    2: 'Die Vereinbarung wurde am 15. März 2023 unterschireben.',
    3: 'Kapitel 1: Einleitung\nDieser Text behandelt das Thema OCR. \n- Punkt 1\n- Punkt 2',
    4: 'Die Forschungsergebnisse zeigen, dass...'
  };

  const corrections = {
    1: 'Das wird ein <span style="background-color: #969595; padding: 2px; border-radius: 3px; font-weight: bold;">intensives</span> Jahr.',
    2: 'Die Vereinbarung wurde am 15. März 2023 <span style="background-color: #969595; padding: 2px; border-radius: 3px; font-weight: bold;">unterschrieben</span>.',
    3: '<span style="background-color: #969595; padding: 2px; border-radius: 3px; font-weight: bold;">Kapitel 1: Einleitung<br><br>Dieser Text behandelt das Thema OCR.<br><br>- Punkt 1<br>- Punkt 2</span>',
    4: 'Die Forschungsergebnisse zeigen, dass<span style="background-color: #969595; padding: 2px; border-radius: 3px; font-weight: bold;"> die Effizienz der neuen Methode signifikant höher ist.</span>'
  };

  function checkAnswer(id, expectedValue) {
    const selectElem = document.getElementById(`select-${id}`);
    const feedbackElem = document.getElementById(`feedback-${id}`);
    const textElem = document.getElementById(`text-${id}`);
    const cardElem = document.getElementById(`card-${id}`);

    if (selectElem.value === expectedValue) {
      feedbackElem.textContent = "✓ Korrekt repariert!";
      feedbackElem.style.color = "#5fb079";
      textElem.innerHTML = corrections[id];
      selectElem.disabled = true; 
    } else if (selectElem.value !== "") {
      feedbackElem.textContent = "✗ Falsche Kategorie. Bitte versuchen Sie es erneut.";
      feedbackElem.style.color = "#b05f67";
    } else {
      feedbackElem.textContent = "";
      cardElem.style.borderColor = "#ccc";
      cardElem.style.backgroundColor = "#fcfcfc";
    }
  }

  function resetGame() {
    for (let i = 1; i <= 4; i++) {
      document.getElementById(`select-${i}`).value = "";
      document.getElementById(`select-${i}`).disabled = false;
      document.getElementById(`feedback-${i}`).textContent = "";
      document.getElementById(`card-${i}`).style.borderColor = "#ccc";
      document.getElementById(`text-${i}`).innerText = originalTexts[i];
    }
  }
</script>

### Fazit

Die OCR-Nachbearbeitung ist ein entscheidender Schritt, um sicherzustellen, dass digitalisierte Texte korrekt und nützlich sind. Obwohl die OCR-Technologie kontinuierlich verbessert wird, bleibt die Nachbearbeitung ein wichtiger Bestandteil des Workflows zur Textdigitalisierung. Indem Sie sorgfältig Erkennungsfehler korrigieren, Tippfehler und Grammatik überprüfen, die Formatierung wiederherstellen und die Vollständigkeit sicherstellen, können Sie die Qualität Ihrer digitalisierten Dokumente erheblich verbessern.
