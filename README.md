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
            /* Animated background */
            background: linear-gradient(45deg, #4CAF50, #2196F3, #f44336, #ffeb3b);
            background-size: 400% 400%;
            animation: colorAnimation 15s ease infinite;
            color: #333; /* Default text color */
        }

        @keyframes colorAnimation {
            0% {background-position: 0% 50%;}
            50% {background-position: 100% 50%;}
            100% {background-position: 0% 50%;}
        }

        h1 {
            color: #fff; /* White color for the heading for better contrast */
            margin-bottom: 20px;
            text-align: center;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3); /* Subtle text shadow */
        }

        textarea {
            width: 80%;
            min-height: 150px;
            margin-bottom: 10px;
            padding: 10px;
            border: 1px solid #ccc;
            box-sizing: border-box;
            border-radius: 8px; /* Rounded corners for textarea */
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        button {
            padding: 12px 25px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            margin-bottom: 20px;
            border-radius: 5px; /* Rounded corners for button */
            font-size: 16px;
            transition: background-color 0.3s ease; /* Smooth transition for hover effect */
        }

        button:hover {
            background-color: #45a049; /* Darker green on hover */
        }

        table {
            width: 80%;
            border-collapse: collapse;
            margin-top: 20px;
            background-color: rgba(255, 255, 255, 0.9); /* Slightly transparent white background for the table */
            box-shadow: 0 4px 15px rgba(0,0,0,0.2); /* More pronounced shadow */
            border-radius: 10px; /* More rounded corners */
            overflow: hidden; /* Ensures content respects border-radius */
        }

        th, td {
            border: 1px solid #ddd;
            padding: 10px; /* Slightly more padding */
            text-align: right;
        }

        th {
            background-color: #e0e0e0; /* Lighter grey for headers */
            font-weight: bold;
            color: #555;
        }

        tr:nth-child(even) {
            background-color: #f9f9f9; /* Zebra striping for table rows */
        }

        tr:hover {
            background-color: #e9e9e9; /* Highlight row on hover */
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
            tableContainer.innerHTML = ""; // Clear any previous table

            if (lines.length > 0) {
                const table = document.createElement("table");
                const thead = document.createElement("thead");
                const tbody = document.createElement("tbody");
                const headerRow = document.createElement("tr");

                // Assume the first line contains comma-separated headers
                const headers = lines.shift().split(',').map(header => header.trim()); // Get headers and remove from lines
                headers.forEach(headerText => {
                    const th = document.createElement("th");
                    th.textContent = headerText;
                    headerRow.appendChild(th);
                });
                thead.appendChild(headerRow);
                table.appendChild(thead);

                // Add data rows to the table
                lines.forEach(line => {
                    const rowData = line.split(',').map(data => data.trim());
                    const tr = document.createElement("tr");
                    rowData.forEach(cellData => {
                        const td = document.createElement("td");
                        td.textContent = cellData;
                        tr.appendChild(td);
                    });
                    tbody.appendChild(tr);
                });
                table.appendChild(tbody);
                tableContainer.appendChild(table);
            } else {
                tableContainer.textContent = "الرجاء إدخال نص لإنشاء الجدول.";
            }
        }
    </script>
</body>
</html>
