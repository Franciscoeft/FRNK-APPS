<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>MacroBot Frank</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 2rem;
      background: #f0f4f8;
      color: #333;
    }
    h1 {
      text-align: center;
    }
    label, input, textarea {
      display: block;
      width: 100%;
      margin-bottom: 1rem;
    }
    button {
      padding: 0.5rem 1rem;
      cursor: pointer;
    }
    #output {
      white-space: pre;
      background: #fff;
      padding: 1rem;
      border: 1px solid #ccc;
      overflow: auto;
      max-height: 300px;
    }
  </style>
</head>
<body>
  <h1>🚗 MacroBot Frank</h1>
  <p>Sube un archivo <strong>.txt</strong> con un VIN por línea. El bot generará automáticamente tu archivo HAScript.</p>
  <label for="fileInput">Selecciona tu archivo de VINs (.txt):</label>
  <input type="file" id="fileInput" accept=".txt" />

  <label for="codigo1">Código fijo (ej. fdfv000001):</label>
  <input type="text" id="codigo1" value="fdfv000001" />

  <label for="codigo2">Fecha fija (ej. 061925):</label>
  <input type="text" id="codigo2" value="061925" />

  <button onclick="generarMacro()">Generar Macro</button>
  <a id="downloadLink" style="display:none" download="macro_generado_vins.HAScript">Descargar Macro</a>

  <h2>Vista previa:</h2>
  <div id="output"></div>

  <script>
    function generarMacro() {
      const fileInput = document.getElementById("fileInput");
      const codigo1 = document.getElementById("codigo1").value;
      const codigo2 = document.getElementById("codigo2").value;
      const output = document.getElementById("output");
      const reader = new FileReader();

      if (!fileInput.files[0]) return alert("Selecciona un archivo .txt con VINs");

      reader.onload = function (e) {
        const lines = e.target.result.trim().split(/\r?\n/).filter(l => l);
        let macro = `<HAScript name="macro_vins_generado" description="" timeout="60000" pausetime="300" promptall="true" blockinput="true" author="Frank" creationdate="Jun 19, 2025" supressclearevents="false" usevars="false" ignorepauseforenhancedtn="true" delayifnotenhancedtn="0" ignorepausetimeforenhancedtn="true" continueontimeout="false">\n`;

        lines.forEach((vin, i) => {
          const id = String(i + 1).padStart(3, '0');
          const next = String(i + 2).padStart(3, '0');
          macro += `\n    <screen name="Screen1_${id}" entryscreen="true" exitscreen="false" transient="false">\n        <description >\n            <oia status="NOTINHIBITED" optional="false" invertmatch="false" />\n        </description>\n        <actions>\n            <input value="[pf11]" row="0" col="0" movecursor="true" xlatehostkeys="true" encrypted="false" />\n        </actions>\n        <nextscreens timeout="0" >\n            <nextscreen name="Screen2_${id}" />\n        </nextscreens>\n    </screen>\n\n    <screen name="Screen2_${id}" entryscreen="false" exitscreen="false" transient="false">\n        <description >\n            <oia status="NOTINHIBITED" optional="false" invertmatch="false" />\n            <numfields number="163" optional="true" invertmatch="false" />\n            <numinputfields number="4" optional="true" invertmatch="false" />\n        </description>\n        <actions>\n            <input value="${vin}[up]${codigo1}[down][down][down][down][down][down][down][down]${codigo2}[field+][enter]" row="0" col="0" movecursor="true" xlatehostkeys="true" encrypted="false" />\n        </actions>\n        <nextscreens timeout="0" >\n            <nextscreen name="Screen3_${id}" />\n        </nextscreens>\n    </screen>\n\n    <screen name="Screen3_${id}" entryscreen="false" exitscreen="false" transient="false">\n        <description >\n            <oia status="NOTINHIBITED" optional="false" invertmatch="false" />\n        </description>\n        <actions>\n            <input value="[enter]" row="0" col="0" movecursor="true" xlatehostkeys="true" encrypted="false" />\n        </actions>\n        <nextscreens timeout="0" >\n            <nextscreen name="Screen4_${id}" />\n        </nextscreens>\n    </screen>\n\n    <screen name="Screen4_${id}" entryscreen="false" exitscreen="false" transient="false">\n        <description >\n            <oia status="NOTINHIBITED" optional="false" invertmatch="false" />\n        </description>\n        <actions>\n            <input value="[pf5]" row="0" col="0" movecursor="true" xlatehostkeys="true" encrypted="false" />\n        </actions>\n        <nextscreens timeout="0" >\n            <nextscreen name="Screen1_${next}" />\n        </nextscreens>\n    </screen>`;
        });

        macro += `\n</HAScript>`;
        output.textContent = macro;

        const blob = new Blob([macro], { type: 'text/plain' });
        const url = URL.createObjectURL(blob);
        const link = document.getElementById("downloadLink");
        link.href = url;
        link.style.display = "inline-block";
        link.textContent = "⬇ Descargar Macro generado";
      };

      reader.readAsText(fileInput.files[0]);
    }
  </script>
</body>
</html>
