<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
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
            height: 50px; /* Cria espaço para o conteúdo */
        }
        .index-column {
            width: 10%; /* Ajuste a largura conforme necessário */
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

        /* Alinhamento das tabelas de fotos */
        .photo-table th, .photo-table td {
            width: 50%; /* A largura das colunas de fotos agora será igualmente distribuída */
        }

        .defect-set {
            margin-bottom: 20px;
        }

        /* Estilo para a imagem de pré-visualização */
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

            <!-- Adicionando as caixas de seleção para Typ e Projekt abaixo de Standort Nr -->
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

            <!-- Conjunto de defeitos e fotos -->
            <div id="defect-container">
                <!-- As tabelas de defeitos serão adicionadas aqui -->
            </div>

            <!-- Botão para adicionar mais defeitos e fotos -->
            <button type="button" onclick="addDefect()">+</button>
        </div>

        <!-- Nova tabela adicionada antes da seção Unterschriften -->
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
            
            <!-- Novo campo de seleção para o GU -->
            <label for="gu">GU Auswahl:</label>
            <select id="gu" name="gu">
                <option value="Gimbel">Gimbel</option>
                <option value="Constructure">Constructure</option>
                <option value="Other">Other</option>
                <option value="Intern">Intern</option>
            </select>
        </div>

        <div class="send-button">
            <a href="mailto:hugo.vasconcellos@americantower.com?subject=Prüfprotokoll&body=Hier%20ist%20das%20Protokoll%20für%20die%20Überprüfung." target="_blank">
                <button type="button">Protokoll absenden</button>
            </a>
        </div>
    </div>

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

        // Função para remover uma linha
        function removeRow(button) {
            var row = button.parentNode.parentNode;
            row.parentNode.removeChild(row);
        }

        // Função para adicionar um conjunto de defeitos e fotos
        function addDefect() {
            var container = document.getElementById('defect-container');

            // Cria o novo conjunto (tabela de defeito + tabela de fotos)
            var defectSet = document.createElement('div');
            defectSet.classList.add('defect-set');

            // Defeito - tabela
            var defectTable = 
                `<table class="defect-table">
                    <tr>
                        <th class="index-column">Index</th>
                        <th>Mängel - Kategorie/Kurzbeschreibung</th>
                        <th>X – Mangel<br>M – Major</th>
                    </tr>
                    <tr>
                        <td><input type="text" placeholder="X.XX"></td>
                        <td><input type="text" placeholder="Mängel-Kategorie"></td>
                        <td>
                            <select>
                                <option value="X">X – Mangel</option>
                                <option value="M">M – Major</option>
                            </select>
                        </td>
                    </tr>
                </table>`;

            // Fotos - tabela
            var photoTable = 
                `<table class="photo-table">
                    <tr>
                        <th>Fotos (aktueller Mangel)</th>
                        <th>Fotos (nach Mangelkorrektur)</th>
                    </tr>
                    <tr>
                        <td style="height: 200px;">
                            <input type="file" accept="image/*" onchange="previewImage(event, this)">
                            <img class="preview" src="" alt="Preview">
                        </td>
                        <td style="height: 200px;">
                            <input type="file" accept="image/*" onchange="previewImage(event, this)">
                            <img class="preview" src="" alt="Preview">
                        </td>
                    </tr>
                </table>`;

            // Botão de remoção
            var removeButton = `<button type="button" onclick="removeDefect(this)">-</button>`;

            // Adiciona a tabela de defeito, fotos e o botão de remoção ao conjunto
            defectSet.innerHTML = defectTable + photoTable + removeButton;

            // Adiciona o novo conjunto ao container
            container.appendChild(defectSet);
        }

        // Função para remover o conjunto de defeito e fotos
        function removeDefect(button) {
            var defectSet = button.parentElement;
            defectSet.remove();
        }

        // Função para exibir a imagem de pré-visualização
        function previewImage(event, input) {
            var reader = new FileReader();
            reader.onload = function () {
                var img = input.nextElementSibling; // Imagem que estará no HTML após o input
                img.src = reader.result; // Define a imagem de pré-visualização
            };
            reader.readAsDataURL(event.target.files[0]);
        }
    </script>
</body>
</html>
