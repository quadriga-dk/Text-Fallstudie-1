# LLM-basierte OCR-Nachbearbeitung

Natürlich gibt es auch intelligentere Methoden zur Nachbearbeitung von OCR-Ergebnissen. Diese Methoden basieren auf datengesteuerten maschinellen Lerntechniken. Zum Beispiel können große Sprachmodelle manchmal sehr gut bei der Nachkorrektur von OCR-Ergebnissen abschneiden. Es ist jedoch wichtig, sich ihrer Risiken und Einschränkungen bewusst zu sein.

* Große Sprachmodelle erfordern viele Ressourcen (Rechenressourcen, Energieressourcen, Speicherressourcen) zum Betrieb. Sie können nicht auf einem Personalcomputer ausgeführt werden und werden typischerweise als Dienst mit eingeschränktem Zugriff angeboten. Sie haben auch technische Beschränkungen hinsichtlich der Größe von Eingabe und Ausgabe. Daher könnte es eine große Herausforderung sein, ein großes Korpus zu verarbeiten.
* Ein ungenauer Prompt kann dazu führen, dass das Modell Text generiert, der im Original nicht vorhanden war. Im Folgenden verwenden wir GPT-4, um Beispiele zu generieren:

```{figure} ../assets/images/llm_postcorr_bad.png
---
height: 600px
name: LLM postcorrection gone wrong
---
```

*In diesem Fall haben wir das Modell einfach gebeten, zu „korrigieren“, und als Ergebnis erhielten wir einen Text, der erheblich verändert wurde. Dabei war unser Ziel eigentlich, nur die OCR-Fehler zu korrigieren, ohne den Originaltext zu ändern.*

* Versuchen Sie, detailliertere Anweisungen zu geben, um die gewünschten Ergebnisse zu erhalten.

```{figure} ../assets/images/llm_postcorr_good.png
---
height: 600px
name: LLM postcorrection gone well
---
```
* Sprachmodelle sind von Natur aus nicht deterministisch, sodass die Ergebnisse von Zeit zu Zeit variieren können. Sogar geringfügige und scheinbar harmlose Änderungen des Prompts können dazu führen, dass sie Halluzinationen erzeugen.


```{figure} ../assets/images/llm_postcorr_hallucinates.png
---
height: 600px
name: LLM postcorrection small hallucination
---
```

## 🚀 Your turn: Interaktives Beispiel

The interactive widget below demonstrate the challenges of using LLMs for OCR correction we just saw above. You can also test different prompt strategies and see exactly how AI unpredictability affects the final text!

*⚠️ Note: The widgets below are just simulations designed to replicate LLM behavior, and non-determinism based on pre-computed data.*

```{raw} html
<p style="font-size: 1.3rem;">🎯 <strong> Mini Demo: The LLM Prompt Simulator </strong><br></p>
<p> Unlike rule-based scripts, LLMs are unpredictable. Select different prompt strategies from the dropdown below to see how the model reacts to the raw OCR text. Pay attention to the highlighted words to spot where the LLM makes good corrections (green) and where it "hallucinates" or alters the historical meaning (re/yellow).</p>

<div style="border: 1px solid #ddd; padding: 20px; border-radius: 8px; font-family: sans-serif;">
  
  <div style="margin-bottom: 20px; padding: 15px; border-radius: 8px;">
    <strong style="font-size: 1.1em;">1. Select Prompt Strategy:</strong><br><br>
    <select id="prompt-selector" onchange="updateSimulator()" style="width: 100%; padding: 10px; font-size: 1em; border-radius: 5px; border: 1px solid #ccc; cursor: pointer;">
      <option value="vague">Scenario A: Minimal Prompt (High Risk)</option>
      <option value="detailed">Scenario B: Detailed Prompt (Best Result)</option>
      <option value="regenerate">Scenario C: Regenerating the Detailed Prompt (Non-Determinism)</option>
    </select>
  </div>

  <div style="margin-bottom: 20px;">
    <strong>2. Prompt sent to the LLM:</strong>
    <div id="sim-prompt-box" style="background-color: #f8f9fa; border-left: 4px solid #007bff; padding: 12px; margin-top: 8px; font-family: monospace; white-space: pre-wrap; color: #333;">
      </div>
  </div>

  <div>
    <strong>3. Generated LLM Output:</strong>
    <div id="sim-output-box" style="background-color: #ffffff; border: 1px solid #ced4da; padding: 15px; border-radius: 5px; font-family: Georgia, serif; font-size: 1.1em; line-height: 1.6; color: #333; margin-top: 8px; white-space: pre-wrap;">
      </div>
  </div>
  
  <div id="sim-explanation" style="margin-top: 15px; padding: 10px; border-radius: 5px; font-size: 0.95em; font-weight: bold;">
      </div>

</div>

<script>

  const scenarios = {
    vague: {
      prompt: "Please correct",
      output: "<span style='background-color: #f8d7da; color: #721c24; padding: 2px 4px; border-radius: 3px; font-weight: bold;' title='Hallucination: Changed original phrasing'>Die Grippewelle breitet sich weiter aus</span>\n\nZunahme der schweren Fälle in Berlin.\n\nDie Zahl der Grippefälle ist in den letzten beiden Tagen auch in Groß-Berlin noch erheblich gestiegen. Die <span style='background-color: #f8d7da; color: #721c24; padding: 2px 4px; border-radius: 3px; font-weight: bold;' title='Hallucination: Changed Warenhäuser to Krankenhäuser'>Krankenhäuser</span> und sonstigen großen Geschäfte, die Kriegs- und die privaten Betriebe klagen, dass übermäßig viele Angestellte sich krank melden müssen. Auch bei der Post und bei der Straßenbahn ist der <span style='background-color: #f8d7da; color: #721c24; padding: 2px 4px; border-radius: 3px; font-weight: bold;' title='Hallucination: Changed original phrasing'>Ausfall</span> der Grippekranken bedeutend.",
      explanation: "⚠️ <strong>Danger:</strong> A vague prompt causes the LLM to rewrite the text in its own modern words rather than just fixing OCR errors. It hallucinated 'Krankenhäuser' (hospitals) instead of 'Warenhäuser' (department stores)!",
      expColor: "#f8d7da",
      expTextColor: "#721c24"
    },
    detailed: {
      prompt: "Du bist Deutsch-Muttersprachler. Hier ist ein OCR-Ergebnis in Deutsch. Bitte korrigiere es nach, indem Sie die ursprünglichen Wörter wiederherstellen, die mit Fehlern erkannt wurden.\n\n[Raw OCR text provided...]",
      output: "Hier ist der korrigierte Text:\n\n<span style='background-color: #d4edda; color: #155724; padding: 2px 4px; border-radius: 3px; font-weight: bold;'>Die Grippe wütet weiter</span>\n\nZunahme der schweren Fälle in Berlin.\n\nDie Zahl der Grippefälle ist in den letzten\nbeiden Tagen auch in Groß-Berlin noch \nerheblich gestiegen. Die <span style='background-color: #d4edda; color: #155724; padding: 2px 4px; border-radius: 3px; font-weight: bold;'>Warenhäuser</span> und son-\nstigen großen Geschäfte, die Kriegs- und die privaten\nBetriebe klagen, dass übermäßig viele Angestellte\nsich haben krankmelden müssen, und auch\nbei der Post und bei der Straßenbahn ist der \nAusfall der Grippekranken bedeutend groß.",
      explanation: "✅ <strong>Success:</strong> By defining a clear persona and explicit rules ('restore original words'), the model successfully corrected the OCR noise without changing the historical meaning.",
      expColor: "#d4edda",
      expTextColor: "#155724"
    },
    regenerate: {
      prompt: "Sie sind ein gebildeter deutscher Muttersprachler. Hier ist ein OCR Ergebnis einer deutschen Zeitung aus dem Jahr 1918. Bitte korrigieren Sie es nachträglich, indem Sie die ursprünglichen Wörter wiederherstellen...\n\n[Raw OCR text provided...]",
      output: "Hier ist der korrigierte Text:\n\nDie Grippe wütet weiter\n\nZunahme der schweren Fälle in Berlin.\n\nDie Zahl der Grippefälle ist in den letzten beiden Tagen auch in Groß-Berlin noch erheblich gestiegen. Die <span style='background-color: #fff3cd; color: #856404; padding: 2px 4px; border-radius: 3px; font-weight: bold;' title='Non-deterministic error'>Krankenhäuser</span> und sonstigen großen Geschäfte, die Kriegs- und die privaten Betriebe klagen, dass übermäßig viele Angestellte sich haben krankmelden müssen, und auch bei der Post und bei der Straßenbahn ist der Ausfall der Grippekranken bedeutend groß.",
      explanation: "🎲 <strong>The Non-Determinism Problem:</strong> Even with a highly detailed prompt, running it a second time generated a slightly different result. The LLM randomly brought back the 'Krankenhäuser' mistake.",
      expColor: "#fff3cd",
      expTextColor: "#856404"
    }
  };

  function updateSimulator() {
    const selected = document.getElementById('prompt-selector').value;
    const data = scenarios[selected];

    document.getElementById('sim-prompt-box').innerText = data.prompt;
    document.getElementById('sim-output-box').innerHTML = data.output;
    
    const expBox = document.getElementById('sim-explanation');
    expBox.innerHTML = data.explanation;
    expBox.style.backgroundColor = data.expColor;
    expBox.style.color = data.expTextColor;
  }

  updateSimulator();
</script>
```