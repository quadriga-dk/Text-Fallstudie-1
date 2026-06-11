# Messung der OCR-Qualität

In Bezug auf die optische Zeichenerkennung (OCR) werden Präzision, Recall und F-Maß zur Bewertung der Genauigkeit und Effizienz von OCR-Systemen verwendet. Diese Metriken helfen zu verstehen, wie gut ein OCR-System arbeitet, insbesondere in Bezug auf die korrekte Identifizierung von Zeichen, Wörtern oder spezifischen Informationen in Dokumenten. Hier ist, wie diese Metriken auf die Qualitätsevaluation von OCR angewendet werden:

### Präzision in der OCR
Bei der OCR misst die Präzision die Genauigkeit des erkannten Textes im Vergleich zum tatsächlichen Text in den Dokumentenbildern. Sie berechnet den Anteil der korrekt erkannten Zeichen oder Wörter an allen Zeichen oder Wörtern, die vom OCR-System identifiziert wurden. Hohe Präzision bedeutet, dass die meisten vom OCR-System als vorhanden erkannten Texte tatsächlich korrekt sind, was auf weniger falsch-positive Erkennungen hinweist (d.h. falsch als vorhanden identifiziert).

$$
\text{Präzision (OCR)} = \frac{\text{Korrekt erkannte Zeichen oder Wörter}}{\text{Gesamtzahl erkannter Zeichen oder Wörter}} 
$$

### Recall in der OCR
Recall im Kontext der OCR misst die Fähigkeit des OCR-Systems, alle relevanten Zeichen oder Wörter aus den Dokumentenbildern zu erfassen. Es ist das Verhältnis der korrekt identifizierten Zeichen oder Wörter zu allen Zeichen oder Wörtern, die tatsächlich in den Dokumenten vorhanden sind. Hoher Recall zeigt an, dass das OCR-System in der Lage ist, die meisten tatsächlich vorhandenen Texte zu erkennen, wodurch falsch-negative Erkennungen minimiert werden (d.h. das Versäumnis, vorhandenen Text zu erkennen).

$$
\text{Recall (OCR)} = \frac{\text{Korrekt erkannte Zeichen oder Wörter}}{\text{Gesamtzahl der tatsächlichen Zeichen oder Wörter in den Dokumenten}}
$$

### F1-Score in der OCR
Der F1-Score in der OCR bietet eine einzelne Metrik, die sowohl Präzision als auch Recall kombiniert, um eine ausgewogene Ansicht der Gesamtleistung des OCR-Systems zu geben. Da Präzision und Recall einen Trade-off haben (die Verbesserung des einen kann oft zu einer Verringerung des anderen führen), hilft der F1-Score dabei, die Effektivität des OCR-Systems bei der genauen Texterkennung und der Minimierung sowohl von falsch-positiven als auch von falsch-negativen Erkennungen zu bewerten.

$$
\text{F1-Score (OCR)} = 2 \times \frac{\text{Präzision (OCR)} \times \text{Recall (OCR)}}{\text{Präzision (OCR)} + \text{Recall (OCR)}}
$$

Diese Metriken sind entscheidend für die Bewertung von OCR-Systemen, insbesondere in Anwendungen, bei denen die Genauigkeit der Texterkennung direkt das Ergebnis beeinflusst, wie z.B. bei der Dokumentenautomatisierung, der Datenerfassung aus gescannten Dokumenten und der automatisierten Verarbeitung handschriftlicher Formulare. Ein Gleichgewicht zwischen hoher Präzision und hohem Recall ist oft gewünscht, um sicherzustellen, dass das OCR-System sowohl genau als auch umfassend in seinen Texterkennungsfähigkeiten ist.

### Understanding Precision, Recall & F1 Intuitively

The interactive visualization below serves as an operational demo of the introduced metrics of Precision, Recall, and F1-score at the character level within a controlled, simulated OCR setting. Rather than only considering aggregated metric values, the visualization shows how individual recognition errors (substitutions, deletions, and insertions) directly affect Precision, Recall, and F1.

The confusion matrix represents the distribution of correctly recognized characters (true positives), incorrectly recognized characters (false positives), and missed characters (false negatives). Based on this distribution, the corresponding evaluation metrics are calculated dynamically.



```{raw} html
<div id="toy-ocr" style="font-family:system-ui, sans-serif; max-width:650px; margin:15px 0;">
  <h3 style="margin-bottom:20px;">🎯 Mini Demo: Enter a string and and move the slider to see how each metrics change</h3>

  <!-- GT input -->
  <label>Enter a text (Ground truth):</label>
  <input id="toyGT" value="BERLIN"
                    maxlength="20"
                    style="margin-left:6px; padding:4px; font-size:1rem; width:120px;"/>
  <span style="margin-left:9px; font-size:0.85rem; color:#666; font-style:italic;">
        (max 20 characters)
  </span>


  <!-- Slider -->
  <div style="margin-top:15px;">
    <p> At low recognition accuracy, a larger number of characters is typically missed leading to low recall, while precision may still remain relatively high         if only few incorrect characters are inserted. As the recognition accuracy increases, recall generally improves and the operating point in the                 Precision–Recall diagram changes accordingly.</p>
    <label>Simulated OCR accuracy:</label>
    <input id="toySlider" type="range" min="0" max="100" step="5" value="80" 
           style="width:250px; margin-left:10px;">
    <span id="toySliderVal">80%</span>
  </div>

  <!-- OCR output -->
  <div style="margin-top:15px;">
    <strong>Simulated OCR output:</strong>
    <div id="toyOCR" 
         style="margin-top:8px; padding:8px; border:1px solid #ccc; border-radius:4px; font-family:monospace; background:#fafafa;">
    </div>
  </div>

  <div style="display:flex; align-items:center; gap:12px; margin-top:15px;">

  <div id="confMatrix" style="display:grid; grid-template-columns:1fr 1fr; gap:6px; width:220px; text-align:center; font-weight:600;">
    <div id="cmTP" title="True Positive: Character correctly recognized by the OCR system. Example: GT (B) → OCR (B)"
         style="padding:8px; border-radius:6px; cursor:help;"></div>

    <div id="cmFP" title="False Positive: Character incorrectly produced by OCR that should not be there. Example: GT (–) → OCR (Z) or GT (B) → OCR (X)"
         style="padding:8px; border-radius:6px; cursor:help;"></div>

    <div id="cmFN" title="False Negative: Character present in the ground truth but missed by OCR. Example: GT (E) → OCR (missing)"
         style="padding:8px; border-radius:6px; cursor:help;"></div>

    <div id="cmTN" title="True Negative: Correct absence of a character where none should appear. Note: Less meaningful in character-level OCR evaluation."
         style="padding:8px; border-radius:6px; cursor:help;"></div>
  </div>

  <div style="font-size:1rem; color:#666; font-style:italic; max-width:180px; margin-left:20px;">
    Move your cursor over the blocks to know more.
  </div>

</div>

  <!-- Metrics -->
  <div id="toyMetrics" style="margin-top:15px; line-height:1.4;"></div>

  <canvas id="prChart" width="420" height="320" style="margin-top:20px; border:1px solid #aaa; background:#111;"></canvas>

  
</div>



<script>
let ocrCache = {};
(function(){
  const gtInput = document.getElementById("toyGT");
  const slider  = document.getElementById("toySlider");
  const sliderVal = document.getElementById("toySliderVal");
  const ocrBox = document.getElementById("toyOCR");
  const metrics = document.getElementById("toyMetrics");

  function pseudoRandom(seed){
  return Math.abs(Math.sin(seed) * 10000) % 1;
  }

  function simulateOCR(gt, accuracy){

  const chars = gt.split("");
  const total = chars.length;
  const correctCount = Math.round(total * (accuracy / 100));
  const errorCount = total - correctCount;
  const errorIndices = [];

  for(let i = 0; i < errorCount; i++){
    let idx = Math.floor(
      pseudoRandom(accuracy + i) * total
    );
    while(errorIndices.includes(idx)){
      idx = (idx + 1) % total;
    }
    errorIndices.push(idx);
  }
  let ocrOut = [];
  chars.forEach((ch, i) => {
    if(!errorIndices.includes(i)){
      ocrOut.push({type:"ok", char:ch});
      return;
    }
    const errorType = Math.floor(
      pseudoRandom(accuracy * (i + 1)) * 3
    );
    if(errorType === 0){
      ocrOut.push({type:"sub", char:"X"});
    }
    else if(errorType === 1){
      ocrOut.push({type:"miss", char:""});
    }
    else{
      ocrOut.push({type:"ins", char:"Z"});
      ocrOut.push({type:"ok", char:ch});
    }
  })
  return ocrOut;
  }

  function computeMetrics(gt, ocrOut){
    const gtLen = gt.length;

    let TP = 0, FP = 0, FN = 0;

    let cleanOCR = ocrOut.filter(x => x.type !== "ins");

    cleanOCR.forEach((item,i)=>{
      if(i >= gtLen) return;
      if(item.type === "ok") TP++;
      else if(item.type === "miss") FN++;
      else if(item.type === "sub") {FP++; FN++;}
    });

    FP += ocrOut.filter(x=>x.type==="ins").length;

    const precision = TP + FP === 0 ? 0 : TP/(TP+FP);
    const recall = TP + FN === 0 ? 0 : TP/(TP+FN);
    const f1 = (precision+recall===0) ? 0 : 2*(precision*recall)/(precision+recall);

    return {TP, FP, FN, precision, recall, f1};
  }

  function render(){

      const gt = gtInput.value.trim().toUpperCase();
      const acc = parseInt(slider.value);
    
      sliderVal.textContent = acc + "%";
    
      const cacheKey = gt + "_" + acc;
    
      if (!ocrCache[cacheKey]) {
        ocrCache[cacheKey] = simulateOCR(gt, acc);
      }
    
      const ocr = ocrCache[cacheKey];
    
      ocrBox.innerHTML = ocr.map(item=>{
        if(item.type==="ok")
          return `<span style="color:#444;">${item.char}</span>`;
        if(item.type==="sub")
          return `<span style="color:white; background:#e74c3c; padding:0 2px;">${item.char}</span>`;
        if(item.type==="miss")
          return `<span style="color:white; background:#3498db; padding:0 4px;">␣</span>`;
        if(item.type==="ins")
          return `<span style="color:black; background:#2ecc71; padding:0 2px;">${item.char}</span>`;
      }).join(" ");
    
      
      const m = computeMetrics(gt, ocr);
    
      metrics.innerHTML = `
        <strong>Precision:</strong> ${m.precision.toFixed(2)}  
        <br><strong>Recall:</strong> ${m.recall.toFixed(2)}  
        <br><strong>F1:</strong> ${m.f1.toFixed(2)}
      `;
    
      
      const TN = gt.length - (m.TP + m.FN);
    
      document.getElementById("cmTP").style.background = "#1f77b4";
      document.getElementById("cmFP").style.background = "#4fa3d1";
      document.getElementById("cmFN").style.background = "#7fbce5";  
      document.getElementById("cmTN").style.background = "#c6e2f5";
    
      document.getElementById("cmTP").style.color = "black";
      document.getElementById("cmFP").style.color = "black";
      document.getElementById("cmFN").style.color = "black";
      document.getElementById("cmTN").style.color = "black";
    
      document.getElementById("cmTP").innerHTML = `TP<br>${m.TP}`;
      document.getElementById("cmFP").innerHTML = `FP<br>${m.FP}`;
      document.getElementById("cmFN").innerHTML = `FN<br>${m.FN}`;
      document.getElementById("cmTN").innerHTML = `TN<br>${TN}`;
    
      drawPRCurve(m.precision, m.recall);
  }

const prCanvas = document.getElementById("prChart");
const ctx = prCanvas.getContext("2d");

function drawPRCurve(p, r){
  ctx.clearRect(0, 0, 420, 320);

  const left = 60;
  const bottom = 280;
  const right = 400;
  const top = 20;

  const width = right - left;
  const height = bottom - top;

  ctx.strokeStyle = "#444";
  ctx.lineWidth = 1;
  for(let i = 0; i <= 5; i++){
    const x = left + i * (width / 5);
    const y = bottom - i * (height / 5);

    ctx.beginPath(); ctx.moveTo(x, top); ctx.lineTo(x, bottom); ctx.stroke();
    ctx.beginPath(); ctx.moveTo(left, y); ctx.lineTo(right, y); ctx.stroke();
  }

  ctx.strokeStyle = "#fff";
  ctx.lineWidth = 2;
  ctx.beginPath();
  ctx.moveTo(left, top);
  ctx.lineTo(left, bottom);
  ctx.lineTo(right, bottom);
  ctx.stroke();

  ctx.fillStyle = "#fff";
  ctx.font = "12px system-ui";
  for(let i = 0; i <= 5; i++){
    const val = (i / 5).toFixed(1);

    const x = left + i * (width / 5);
    ctx.fillText(val, x - 6, bottom + 18);

    const y = bottom - i * (height / 5);
    ctx.fillText(val, left - 40, y + 4);
  }

  ctx.fillText("Recall →", left + width / 2 - 20, bottom + 35);

  ctx.save();
  ctx.translate(10, top + height / 2 + 20);
  ctx.rotate(-Math.PI / 2);
  ctx.fillText("Precision →", 0, 0);
  ctx.restore();

  ctx.strokeStyle = "#888";
  ctx.setLineDash([6,6]);
  ctx.beginPath();
  ctx.moveTo(left, bottom);
  ctx.lineTo(right, top);
  ctx.stroke();
  ctx.setLineDash([]);

  const f1Levels = [0.3, 0.5, 0.7, 0.9];
  ctx.strokeStyle = "#666";
  ctx.setLineDash([4,6]);
  ctx.lineWidth = 1;

  f1Levels.forEach(F1 => {
    ctx.beginPath();
    let started = false;

    for(let r = 0.01; r <= 1; r += 0.01){
      const p = (F1 * r) / (2*r - F1); 
      if(p > 0 && p <= 1){
        const x = left + r * width;
        const y = bottom - p * height;

        if(!started){
          ctx.moveTo(x, y);
          started = true;
        } else {
          ctx.lineTo(x, y);
        }
      }
    }

    ctx.stroke();
  });

  ctx.setLineDash([]);

  const x = left + r * width;
  const y = bottom - p * height;

  ctx.fillStyle = "#ff4757";
  ctx.beginPath();
  ctx.arc(x, y, 7, 0, Math.PI * 2);
  ctx.fill();

  window.prDot = {x, y, p, r};
}


prCanvas.addEventListener("mousemove", function(e){
  const rect = prCanvas.getBoundingClientRect();
  const mx = e.clientX - rect.left;
  const my = e.clientY - rect.top;

  if(!window.prDot) return;

  const dx = mx - window.prDot.x;
  const dy = my - window.prDot.y;

  if(Math.sqrt(dx*dx + dy*dy) < 8){
    prCanvas.title = 
      `Precision: ${window.prDot.p.toFixed(2)} | Recall: ${window.prDot.r.toFixed(2)}`;
  } else {
    prCanvas.title = "";
  }
});

  slider.addEventListener("input", render);
  gtInput.addEventListener("input", () => {
    ocrCache = {};
    render();
  });

  render();
})();

</script>

```

The visualization also illustrates that high precision alone does not necessarily imply high overall OCR quality if recall remains low. Conversely, improving recall can introduce additional false positives, which may reduce precision. The F1-score captures this balance between both tendencies.
In this way, the visualization highlights that similar F1-scores can arise from different combinations of precision and recall, corresponding to distinct OCR error behaviors.