# zcmoda1
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
            max-width: 500px;
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
    </style>
</head>
<body>
    <h1>服装成本计算器</h1>

    <label for="fabricPrice">面料价格（元/米）：</label>
    <input type="number" id="fabricPrice" placeholder="请输入每米面料价格">

    <label for="fabricUsage">用料（米）：</label>
    <input type="number" id="fabricUsage" placeholder="请输入每件衣服所需用料">

    <label for="laborCost">人工成本（元/件）：</label>
    <input type="number" id="laborCost" placeholder="请输入人工成本">

    <label for="otherCosts">其他成本（元/件）：</label>
    <input type="number" id="otherCosts" placeholder="请输入其他成本，例如包装运输等">

    <button onclick="calculateCost()">计算成本</button>

    <div class="result" id="result"></div>

    <script>
        function calculateCost() {
            const fabricPrice = parseFloat(document.getElementById('fabricPrice').value) || 0;
            const fabricUsage = parseFloat(document.getElementById('fabricUsage').value) || 0;
            const laborCost = parseFloat(document.getElementById('laborCost').value) || 0;
            const otherCosts = parseFloat(document.getElementById('otherCosts').value) || 0;

            // 计算面料成本和总成本
            const fabricCost = fabricPrice * fabricUsage;
            const totalCost = fabricCost + laborCost + otherCosts;

            // 显示结果
            document.getElementById('result').innerHTML = `
                <p>面料成本：<strong>￥${fabricCost.toFixed(2)}</strong></p>
                <p>总成本：<strong>￥${totalCost.toFixed(2)}</strong></p>
            `;
        }
    </script>
</body>
</html>
