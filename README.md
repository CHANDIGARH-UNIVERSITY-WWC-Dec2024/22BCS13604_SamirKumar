<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Movie Script Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 0;
        }
        .container {
            max-width: 600px;
            margin: auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 8px;
            background-color: #f9f9f9;
        }
        label, select, input {
            margin-bottom: 10px;
            display: block;
            width: 100%;
        }
        button {
            padding: 10px 20px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        .output {
            margin-top: 20px;
            white-space: pre-wrap;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Movie Script Generator</h1>
        <label for="genre">Select Genre:</label>
        <select id="genre">
            <option value="action">Action</option>
            <option value="romance">Romance</option>
            <option value="comedy">Comedy</option>
        </select>
        <label for="character1">Character 1 Name:</label>
        <input type="text" id="character1" placeholder="Enter name">
        <label for="character2">Character 2 Name:</label>
        <input type="text" id="character2" placeholder="Enter name">
        <button onclick="generateScript()">Generate Script</button>
        <div class="output" id="output"></div>
    </div>
    <script>
        async function generateScript() {
            const genre = document.getElementById("genre").value;
            const character1 = document.getElementById("character1").value || "Alex";
            const character2 = document.getElementById("character2").value || "Jamie";

            const response = await fetch('/generate', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ genre, character1, character2 })
            });
            const data = await response.json();
            document.getElementById("output").textContent = data.script;
        }
    </script>
</body>
</html>
