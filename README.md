<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>面料价格管理</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 20px;
            max-width: 600px;
            background-color: #f9f9f9;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
        }
        .input-group {
            margin-bottom: 10px;
        }
        input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }
        button:hover {
            background-color: #0056b3;
        }
        .fabric-list {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>面料价格管理</h1>
    <div class="input-group">
        <label>面料名称</label>
        <input type="text" id="fabricName">
    </div>
    <div class="input-group">
        <label>面料价格（€/米）</label>
        <input type="number" id="fabricPrice" step="0.01">
    </div>
    <button onclick="saveFabric()">保存面料</button>
    <h2>已保存的面料</h2>
    <div class="fabric-list" id="fabricList"></div>

    <script>
        function saveFabric() {
            const name = document.getElementById('fabricName').value.trim();
            const price = parseFloat(document.getElementById('fabricPrice').value) ||
