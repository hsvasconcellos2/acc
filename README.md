<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prüfprotokoll - Mangelabmeldung</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            line-height: 1.6;
            background-color: #f4f4f9;
            color: #333;
        }
        .container {
            width: 90%;
            margin: 20px auto;
            background: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1, h2 {
            text-align: center;
            color: #0056b3;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        table th, table td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: center;
        }
        table th {
            background-color: #f2f2f2;
            font-weight: bold;
        }
        .section {
            margin-bottom: 20px;
        }
        .highlight {
            background-color: #ffffcc;
        }
        .signature {
            margin-top: 20px;
        }
        table td {
            height: 50px;
        }
        .index-column {
            width: 10%;
        }
        .checkbox-group input[type="checkbox"] {
            margin-right: 8px;
        }
        .send-button {
            text-align: center;
            margin-top: 30px;
        }
        .send-button button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #0056b3;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .send-button button:hover {
            background-color: #004080;
        }
        .photo-table th, .photo-table td {
            width: 50%;
        }
        .preview {
            max-width: 100%;
            max-height: 200px;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>ATC-Prüf u. GU-Mangelabmelde Protokoll</h1>
        <div class="protokoll-container">
            <h2>Protokoll Nr: 
                <select>
                    <option value="V0">V0</option>
                    <option value="V1">V1</option>
                    <option value="V2">V2</option>
                    <option value="V3">V3</option>
                    <option value="V4">V4</option>
                    <option value="V5">V5</option>
                </select>
            </h2>
            <h2>Standort Nr: 
                <input type="text" placeholder="Standort Nr">
            </h2>

            <div class="section">
                <p><strong>Typ:</strong> 
                    <select>
                        <option value="Rooftop">Rooftop</option>
                        <option value="Tower">Tower</option>
                    </select>
                </p>
                <p><strong>Projekt:</strong>
                    <select>
                        <option value="BTS">BTS</option>
                        <option value="Aurora">Aurora</option>
                        <option value="Bravo">Bravo</option>
                    </select>
                </p>
            </div>
        </div>
        
        <div class="section">
            <h2>Standortdetails</h2>
            <table>
                <tr>
                    <th>ATC Standort-Nr</th>
                    <td>123456</td>
                </tr>
                <tr>
                    <th>Kunden Standort-Nr</th>
                    <td>xxx99xxxx</td>
                </tr>
                <tr>
                    <th>Standortadresse</th>
                    <td>Straße, PLZ Ort</td>
                </tr>
            </table>
        </div>

        <div class="section">
            <h2>Prüfung OnSite</h2>
            <div class="checkbox-group">
                <input type="checkbox" id="ja" name="pruefung-onsite">
                <label for="ja">JA</label>
                <input type="checkbox" id="nein" name="pruefung-onsite">
                <label for="nein">NEIN</label>
            </div>
            <p><em>(*bei Onsite Abnahmen muss das zugehörige Protokoll zur Verfügung gestellt werden)</em></p>
        </div>
        
        <div class="section">
            <h2>Prüfungs- Abnahme Ergebnis</h2>
            <div class="checkbox-group">
                <input type="checkbox" id="fehlerfrei" name="abnahme-ergebnis">
                <label for="fehlerfrei">Standort fehlerfrei -> komplett abgenommen</label>
            </div>
            <div class="checkbox-group">
                <input type="checkbox" id="geringfuegige-maengeln" name="abnahme-ergebnis">
                <label for="geringfuegige-maengeln">Standort ABGENOMMEN mit geringfügigen Mängeln</label>
            </div>
            <div class="checkbox-group">
                <input type="checkbox" id="major-maengeln" name="abnahme-ergebnis">
                <label for="major-maengeln">Standort mit Major Mängeln - (Übergabe an Kunden und Betrieb nicht möglich)</label>
            </div>
            <div class="checkbox-group">
                <input type="checkbox" id="critical-maengeln" name="abnahme-ergebnis">
                <label for="critical-maengeln" class="highlight">Standort mit Critical Mängel -> ABNAHME-VERWEIGERUNG</label>
            </div>
        </div>

        <div class="section">
            <h2>Mängel - Übersicht und Fotos</h2>
            <div id="defect-container">
            </div>
            <button type="button" onclick="addDefect()">+</button>
        </div>

        <div class="section">
            <h2>Doku Mängel_Details</h2>
            <table id="mangel-table">
                <thead>
                    <tr>
                        <th>Index</th>
                        <th>Dokumenten Name / Kategorie</th>
                        <th>Mangel Info</th>
                        <th>GU Mangelkorrektur</th>
                        <th>Ação</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td><input type="text" placeholder="Index"></td>
                        <td><input type="text" placeholder="Dokumenten Name / Kategorie"></td>
                        <td><input type="text" placeholder="Mangel Info"></td>
                        <td><input type="text" placeholder="GU Mangelkorrektur"></td>
                        <td><button type="button" onclick="removeRow(this)">-</button></td>
                    </tr>
                </tbody>
            </table>
            <button type="button" onclick="addRow()">+</button>
        </div>

        <div class="signature">
            <h2>Unterschriften</h2>
            <p><strong>Abnahmegewerk:</strong> Vor- Nachname</p>
            <label for="gu">GU Auswahl:</label>
            <select id="gu" name="gu">
                <option value="Gimbel">Gimbel</option>
                <option value="Constructure">Constructure</option>
                <option value="Other">Other</option>
                <option value="Intern">Intern</option>
            </select>
        </div>

        <div class="send-button">
            <!-- Ajustando o botão para ser visível e interativo -->
            <button type="button" onclick="generatePDF()">Gerar PDF e Enviar E-mail</button>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script>
        // Função para adicionar uma nova linha à tabela de documentos
        function addRow() {
            var table = document.getElementById("mangel-table").getElementsByTagName('tbody')[0];
            var newRow = table.insertRow(table.rows.length);
            newRow.innerHTML = 
                `<td><input type="text" placeholder="Index"></td>
                 <td><input type="text" placeholder="Dokumenten Name / Kategorie"></td>
                 <td><input type="text" placeholder="Mangel Info"></td>
                 <td><input type="text" placeholder="GU Mangelkorrektur"></td>
                 <td><button type="button" onclick="removeRow(this)">-</button></td>`;
        }

        // Função para remover uma linha da tabela
        function removeRow(button) {
            var row = button.parentNode.parentNode;
            row.parentNode.removeChild(row);
        }

        // Função para gerar PDF com o conteúdo do formulário
        function generatePDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            doc.setFontSize(18);
            doc.text("ATC-Prüf u. GU-Mangelabmelde Protokoll", 20, 20);

            // Adiciona o conteúdo do formulário no PDF
            doc.setFontSize(12);
            doc.text("Protokoll Nr: " + document.querySelector('select').value, 20, 30);
            doc.text("Standort Nr: " + document.querySelector('input[type="text"]').value, 20, 40);
            doc.text("Typ: " + document.querySelectorAll('select')[1].value, 20, 50);
            doc.text("Projekt: " + document.querySelectorAll('select')[2].value, 20, 60);
            
            doc.text("Standortdetails:", 20, 80);
            doc.autoTable({
                startY: 90,
                head: [['ATC Standort-Nr', 'Kunden Standort-Nr', 'Standortadresse']],
                body: [
                    ['123456', 'xxx99xxxx', 'Straße, PLZ Ort']
                ]
            });

            // Adiciona uma seção de falhas, se necessário
            let defectContainer = document.getElementById("defect-container");
            let defects = defectContainer.getElementsByClassName("defect-row");
            if (defects.length > 0) {
                doc.text("Mängel - Übersicht und Fotos:", 20, 150);
                defects.forEach((defect, index) => {
                    doc.text("Defeito " + (index + 1) + ": " + defect.querySelector("input[name='defect']").value, 20, 160 + (index * 10));
                });
            }

            // Salva o PDF
            doc.save("protokoll.pdf");

            // Abre o Outlook para enviar um e-mail (sem anexar o PDF)
            const email = "recipient@example.com";  // Insira o destinatário do e-mail
            const subject = "Protokoll Mangelabmeldung";
            const body = "Por favor, veja o PDF anexado com o Protokoll.";
            window.location.href = `mailto:${email}?subject=${subject}&body=${body}`;
        }

        // Função para adicionar um defeito ao container
        function
