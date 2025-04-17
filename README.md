<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ترتيب النص في جدول</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }
        textarea {
            width: 80%;
            min-height: 150px;
            margin-bottom: 10px;
            padding: 10px;
            border: 1px solid #ccc;
            box-sizing: border-box;
        }
        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            margin-bottom: 20px;
        }
        table {
            width: 80%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: right;
        }
        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>
    <h1>أدخل النص لترتيبه في جدول</h1>
    <textarea id="inputText" placeholder="أدخل النص هنا (كل سطر سيمثل صفًا في الجدول)"></textarea>
    <button onclick="convertToTable()">إنشاء الجدول</button>
    <div id="tableContainer">
        </div>

    <script>
        function convertToTable() {
            const inputText = document.getElementById("inputText").value;
            const lines = inputText.split('\n').filter(line => line.trim() !== "");
            const tableContainer = document.getElementById("tableContainer");
            tableContainer.innerHTML = ""; // مسح أي جدول سابق

            if (lines.length > 0) {
                const table = document.createElement("table");
                const thead = document.createElement("thead");
                const tbody = document.createElement("tbody");
                const headerRow = document.createElement("tr");

                // افتراض أن السطر الأول يحتوي على رؤوس الأعمدة مفصولة بفواصل (يمكن تعديل هذا)
                const headers = lines[0].split(',').map(header => header.trim());
                headers.forEach(headerText => {
                    const th = document.createElement("th");
                    th.textContent = headerText;
                    headerRow.appendChild(th);
                });
                thead.appendChild(headerRow);
                table.appendChild(thead);

                // إضافة البيانات إلى الجدول
                for (let i = 1; i < lines.length; i++) {
                    const rowData = lines[i].split(',').map(data => data.trim());
                    const tr = document.createElement("tr");
                    rowData.forEach(cellData => {
                        const td = document.createElement("td");
                        td.textContent = cellData;
                        tr.appendChild(td);
                    });
                    tbody.appendChild(tr);
                }
                table.appendChild(tbody);
                tableContainer.appendChild(table);
            } else {
                tableContainer.textContent = "الرجاء إدخال نص لإنشاء الجدول.";
            }
        }
    </script>
</body>
</html>
