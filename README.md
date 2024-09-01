<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>เครื่องคำนวณดัชนีมวลกาย</title>
    <link rel="stylesheet" href="index.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
    <div class="container">
        <h1>เครื่องคำนวณดัชนีมวลกาย (BMI)</h1>
        <label for="weight">น้ำหนัก (กิโลกรัม):</label>
        <input type="number" id="weight" placeholder="กรอกน้ำหนักของคุณ">
        <label for="height">ส่วนสูง (เซนติเมตร):</label>
        <input type="number" id="height" placeholder="กรอกส่วนสูงของคุณ">
        <button onclick="calculateBMI()">คำนวณ BMI</button>
        <div id="result" class="result"></div>
        <canvas id="bmiChart" width="400" height="200"></canvas>
    </div>

    <script>
        var ctx = document.getElementById('bmiChart').getContext('2d');
        var bmiChart = new Chart(ctx, {
            type: 'bar',
            data: {
                labels: ['Underweight', 'Normal weight', 'Overweight', 'Obesity'],
                datasets: [{
                    label: 'BMI Range',
                    data: [18.5, 24.9, 29.9, 40], // Sample data
                    backgroundColor: [
                        'rgba(255, 99, 132, 0.2)',
                        'rgba(54, 162, 235, 0.2)',
                        'rgba(255, 206, 86, 0.2)',
                        'rgba(255, 159, 64, 0.2)'
                    ],
                    borderColor: [
                        'rgba(255, 99, 132, 1)',
                        'rgba(54, 162, 235, 1)',
                        'rgba(255, 206, 86, 1)',
                        'rgba(255, 159, 64, 1)'
                    ],
                    borderWidth: 1
                }]
            },
            options: {
                scales: {
                    y: {
                        beginAtZero: true
                    }
                }
            }
        });

        function calculateBMI() {
            var weight = document.getElementById('weight').value;
            var height = document.getElementById('height').value;

            if (weight && height) {
                height = height / 100; // แปลงส่วนสูงจากเซนติเมตรเป็นเมตร
                var bmi = weight / (height * height);

                var resultText = 'ค่า BMI ของคุณคือ ' + bmi.toFixed(2);

                if (bmi < 18.5) {
                    resultText += ' (น้ำหนักต่ำกว่าเกณฑ์)';
                } else if (bmi < 24.9) {
                    resultText += ' (น้ำหนักปกติ)';
                } else if (bmi < 29.9) {
                    resultText += ' (น้ำหนักเกิน)';
                } else {
                    resultText += ' (โรคอ้วน)';
                }

                document.getElementById('result').innerText = resultText;
            } else {
                document.getElementById('result').innerText = 'กรุณากรอกน้ำหนักและส่วนสูงให้ครบถ้วน';
            }
        }
    </script>
</body>
</html>
