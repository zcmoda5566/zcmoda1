<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>服装成本计算器</title>
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
            font-size: 24px;
            margin-bottom: 20px;
            text-align: center;
        }
        input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
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
        }
        button:hover {
            background-color: #0056b3;
        }
        .result {
            margin-top: 20px;
            font-size: 18px;
            color: #333;
        }
        #imagePreview {
            margin-top: 20px;
            max-width: 200px;
            height: auto;
            display: none;
        }
        #dropArea {
            width: 100%;
            padding: 20px;
            border: 2px dashed #007BFF;
            text-align: center;
            margin-top: 10px;
            cursor: pointer;
        }
        #dropArea:hover {
            background-color: #e9f5ff;
        }
    </style>
</head>
<body>
    <h1>服装成本计算器</h1>

    <div id="dropArea" ondrop="handleDrop(event)" ondragover="handleDragOver(event)">
        拖拽图片到此处或点击上传
        <input type="file" id="sampleImage" accept="image/*" onchange="previewImage(event)" style="display: none;">
    </div>
    <img id="imagePreview" src="" alt="样品预览">

    <label for="fabricName">面料名称：</label>
    <input type="text" id="fabricName" placeholder="请输入面料名称">

    <label for="fabricPrice">面料价格（元/米）：</label>
    <input type="number" id="fabricPrice" placeholder="请输入每米面料价格">

    <label for="fabricUsage">用料（米）：</label>
    <input type="number" id="fabricUsage" placeholder="请输入每件衣服所需用料">

    <label for="laborCost">加工费（元/件）：</label>
    <input type="number" id="laborCost" placeholder="请输入加工费">

    <label for="trimmingCost">包边饰品（元/件）：</label>
    <input type="number" id="trimmingCost" placeholder="请输入包边饰品费用">

    <label for="labelCost">商标牌子（元/件）：</label>
    <input type="number" id="labelCost" placeholder="请输入商标费用">

    <button onclick="calculateCost()">计算成本</button>

    <div class="result" id="result"></div>

    <script>
        function previewImage(event) {
            const reader = new FileReader();
            reader.onload = function () {
                const output = document.getElementById('imagePreview');
                output.src = reader.result;
                output.style.display = 'block';
            }
            reader.readAsDataURL(event.target.files[0]);
        }

        function handleDragOver(event) {
            event.preventDefault();
        }

        function handleDrop(event) {
            event.preventDefault();
            const file = event.dataTransfer.files[0];
            const reader = new FileReader();
            reader.onload = function () {
                const output = document.getElementById('imagePreview');
                output.src = reader.result;
                output.style.display = 'block';
            }
            reader.readAsDataURL(file);
        }

        function calculateCost() {
            const fabricPrice = parseFloat(document.getElementById('fabricPrice').value) || 0;
            const fabricUsage = parseFloat(document.getElementById('fabricUsage').value) || 0;
            const laborCost = parseFloat(document.getElementById('laborCost').value) || 0;
            const trimmingCost = parseFloat(document.getElementById('trimmingCost').value) || 0;
            const labelCost = parseFloat(document.getElementById('labelCost').value) || 0;
            
            const fabricCost = fabricPrice * fabricUsage * 1.05;
            const totalCost = fabricCost + laborCost + trimmingCost + labelCost;

            document.getElementById('result').innerHTML = `
                <p>面料名称：<strong>${document.getElementById('fabricName').value}</strong></p>
                <p>面料成本（含5%）：<strong>￥${fabricCost.toFixed(2)}</strong></p>
                <p>总成本：<strong>￥${totalCost.toFixed(2)}</strong></p>
            `;
        }
    </script>
</body>
</html>
