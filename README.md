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
            max-width: 1000px;
            background-color: #f9f9f9;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
        }
        .container {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }
        .input-group {
            display: flex;
            flex-direction: column;
            width: 30%;
        }
        input {
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
        .result {
            margin-top: 20px;
            font-size: 18px;
            color: #333;
        }
        #dropArea {
            width: 100%;
            padding: 20px;
            border: 2px dashed #007BFF;
            text-align: center;
            margin-bottom: 10px;
        }
        #imagePreview {
            max-width: 100px;
            height: auto;
            display: none;
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
    
    <div class="container">
        <div class="input-group"><label>面料名称</label><input type="text" id="fabricName"></div>
        <div class="input-group"><label>面料价格（€/米）</label><input type="number" id="fabricPrice" step="0.01"></div>
        <div class="input-group"><label>用料（米）</label><input type="number" id="fabricUsage" step="0.01"></div>
        <div class="input-group"><label>加工费（€）</label><input type="number" id="laborCost" step="0.01"></div>
        <div class="input-group"><label>包边饰品（€）</label><input type="number" id="trimmingCost" step="0.01"></div>
        <div class="input-group"><label>商标牌子（€）</label><input type="number" id="labelCost" step="0.01"></div>
        <div class="input-group"><label>衣架（€）</label><input type="number" id="hangerCost" step="0.01"></div>
        <div class="input-group"><label>熨烫（€）</label><input type="number" id="ironingCost" step="0.01"></div>
        <div class="input-group"><label>打纽扣（€）</label><input type="number" id="buttonCost" step="0.01"></div>
        <div class="input-group"><label>染洗（€）</label><input type="number" id="dyeCost" step="0.01"></div>
        <div class="input-group"><label>手工费（€）</label><input type="number" id="manualCost" step="0.01"></div>
        <div class="input-group"><label>皮带（€）</label><input type="number" id="beltCost" step="0.01"></div>
        <div class="input-group"><label>前片印花（€）</label><input type="number" id="printCost" step="0.01"></div>
        <div class="input-group"><label>推荐售卖价格（€）</label><input type="number" id="recommendedPrice" readonly></div>
    </div>
    
    <button onclick="calculateCost()">计算成本</button>
    <div class="result" id="result"></div>
    
    <script>
        function previewImage(event) {
            const reader = new FileReader();
            reader.onload = function () {
                document.getElementById('imagePreview').src = reader.result;
                document.getElementById('imagePreview').style.display = 'block';
            }
            reader.readAsDataURL(event.target.files[0]);
        }
        function handleDragOver(event) { event.preventDefault(); }
        function handleDrop(event) {
            event.preventDefault();
            const file = event.dataTransfer.files[0];
            previewImage({ target: { files: [file] } });
        }
        function calculateCost() {
            const inputs = document.querySelectorAll('input[type=number]');
            inputs.forEach(input => {
                if (input.value.startsWith('.')) {
                    input.value = '0' + input.value;
                }
            });
            
            const fabricPrice = parseFloat(document.getElementById('fabricPrice').value) || 0;
            const fabricUsage = parseFloat(document.getElementById('fabricUsage').value) || 0;
            const laborCost = parseFloat(document.getElementById('laborCost').value) || 0;
            const trimmingCost = parseFloat(document.getElementById('trimmingCost').value) || 0;
            const labelCost = parseFloat(document.getElementById('labelCost').value) || 0;
            const hangerCost = parseFloat(document.getElementById('hangerCost').value) || 0;
            const ironingCost = parseFloat(document.getElementById('ironingCost').value) || 0;
            const buttonCost = parseFloat(document.getElementById('buttonCost').value) || 0;
            const dyeCost = parseFloat(document.getElementById('dyeCost').value) || 0;
            const manualCost = parseFloat(document.getElementById('manualCost').value) || 0;
            const beltCost = parseFloat(document.getElementById('beltCost').value) || 0;
            const printCost = parseFloat(document.getElementById('printCost').value) || 0;
            
            const fabricCost = fabricPrice * fabricUsage * 1.05;
            const totalCost = fabricCost + laborCost + trimmingCost + labelCost + hangerCost + ironingCost + buttonCost + dyeCost + manualCost + beltCost + printCost;
            const recommendedPrice = totalCost * 1.25;
            
            document.getElementById('recommendedPrice').value = recommendedPrice.toFixed(2);
            document.getElementById('result').innerHTML = `<p>总成本：<strong>€${totalCost.toFixed(2)}</strong></p>`;
        }
    </script>
</body>
</html>
