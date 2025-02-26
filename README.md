# ROI-calc-TC
trust center calculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trust Center ROI Calculator</title>
    <!-- Bootstrap CSS for styling -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            padding: 20px;
            background-color: #f8f9fa;
        }
        .calculator-container {
            max-width: 1000px;
            margin: 0 auto;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            padding: 30px;
        }
        .quote-box {
            background-color: #e6f0ff;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 30px;
            font-style: italic;
            color: #0050a0;
        }
        .result-box {
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
        }
        .takeaway-box {
            background-color: #e6f0ff;
            padding: 15px;
            border-radius: 8px;
            margin-top: 20px;
        }
        .takeaway-box h4 {
            color: #0050a0;
        }
        .annual-savings {
            font-weight: bold;
            color: #28a745;
            font-size: 1.2em;
        }
        .input-help {
            font-size: 0.8em;
            color: #6c757d;
            margin-top: 5px;
        }
    </style>
</head>
<body>
    <div class="calculator-container">
        <h2 class="text-center mb-4">Trust Center ROI Calculator</h2>
        
        <div class="quote-box">
            <p class="mb-0">
                "Manually distributing security documentation isn't just inefficient—it's expensive. 
                Calculate exactly how much time and money your team could save with a Trust Center."
            </p>
        </div>

        <div class="row mb-4">
            <div class="col-md-6">
                <h3 class="mb-3">Your Security Documentation Process</h3>
                
                <div class="mb-3">
                    <label for="requestsPerWeek" class="form-label">Security document requests per week</label>
                    <input type="number" class="form-control" id="requestsPerWeek" value="25" min="1">
                    <div class="input-help">Industry average: 25 requests/week for mid-sized companies</div>
                </div>
                
                <div class="mb-3">
                    <label for="minutesPerRequest" class="form-label">Average minutes spent per request</label>
                    <input type="number" class="form-control" id="minutesPerRequest" value="20" min="1">
                    <div class="input-help">Includes time for all stakeholders involved in the process</div>
                </div>
                
                <div class="mb-3">
                    <label for="hourlyRate" class="form-label">Average hourly cost of security personnel ($/hr)</label>
                    <input type="number" class="form-control" id="hourlyRate" value="62.50" min="1" step="0.01">
                    <div class="input-help">Industry average: $62.50/hr for experienced GRC professionals</div>
                </div>
            </div>
            
            <div class="col-md-6">
                <div class="result-box">
                    <h3 class="mb-3 text-primary">Your Trust Center ROI</h3>
                    
                    <div class="mb-4">
                        <h4>Per Single Request:</h4>
                        <div class="d-flex justify-content-between mt-2">
                            <div>Time saved:</div>
                            <div id="singleRequestTime">0.3 hours</div>
                        </div>
                        <div class="d-flex justify-content-between mt-1">
                            <div>Cost saved:</div>
                            <div id="singleRequestMoney">$20.83</div>
                        </div>
                    </div>
                    
                    <div class="mb-4">
                        <h4>Weekly Savings:</h4>
                        <div class="d-flex justify-content-between mt-2">
                            <div>Time saved:</div>
                            <div id="weeklyTime">8.3 hours</div>
                        </div>
                        <div class="d-flex justify-content-between mt-1">
                            <div>Cost saved:</div>
                            <div id="weeklyMoney">$520.83</div>
                        </div>
                    </div>
                    
                    <div class="mb-4">
                        <h4>Monthly Savings:</h4>
                        <div class="d-flex justify-content-between mt-2">
                            <div>Time saved:</div>
                            <div id="monthlyTime">36.1 hours</div>
                        </div>
                        <div class="d-flex justify-content-between mt-1">
                            <div>Cost saved:</div>
                            <div id="monthlyMoney">$2,255.21</div>
                        </div>
                    </div>
                    
                    <div class="pt-2 border-top">
                        <h4 class="text-primary">Annual Savings:</h4>
                        <div class="d-flex justify-content-between mt-2">
                            <div class="fw-bold">Total time saved:</div>
                            <div class="fw-bold" id="annualTime">433.3 hours</div>
                        </div>
                        <div class="d-flex justify-content-between mt-1">
                            <div class="fw-bold">Total cost saved:</div>
                            <div class="annual-savings" id="annualMoney">$27,083.33</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="takeaway-box">
            <h4 class="mb-2">Key Takeaways:</h4>
            <ul class="mb-0">
                <li><strong>Time for value:</strong> 1 document request = <span id="takeSingleTime">0.3</span> hours of your team's time</li>
                <li><strong>Cost per request:</strong> 1 manual document review = <span id="takeSingleMoney">$20.83</span> in hidden labor costs</li>
                <li><strong>Annual impact:</strong> Implementing a Trust Center could save your organization <span id="takeAnnualMoney">$27,083.33</span> per year</li>
            </ul>
        </div>
    </div>

    <script>
        // Function to format currency
        function formatCurrency(value) {
            return '$' + parseFloat(value).toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
        }

        // Function to calculate ROI
        function calculateROI() {
            // Get input values
            const requestsPerWeek = Math.max(1, parseInt(document.getElementById('requestsPerWeek').value) || 0);
            const minutesPerRequest = Math.max(1, parseInt(document.getElementById('minutesPerRequest').value) || 0);
            const hourlyRate = Math.max(1, parseFloat(document.getElementById('hourlyRate').value) || 0);
            
            // Single request calculations
            const singleRequestTimeHours = minutesPerRequest / 60;
            const singleRequestMoney = singleRequestTimeHours * hourlyRate;
            
            // Weekly calculations
            const weeklyTimeHours = requestsPerWeek * singleRequestTimeHours;
            const weeklyMoney = weeklyTimeHours * hourlyRate;
            
            // Monthly calculations (4.33 weeks per month on average)
            const monthlyTimeHours = weeklyTimeHours * 4.33;
            const monthlyMoney = weeklyMoney * 4.33;
            
            // Annual calculations
            const annualTimeHours = weeklyTimeHours * 52;
            const annualMoney = weeklyMoney * 52;
            
            // Update results
            document.getElementById('singleRequestTime').textContent = singleRequestTimeHours.toFixed(1) + ' hours';
            document.getElementById('singleRequestMoney').textContent = formatCurrency(singleRequestMoney);
            
            document.getElementById('weeklyTime').textContent = weeklyTimeHours.toFixed(1) + ' hours';
            document.getElementById('weeklyMoney').textContent = formatCurrency(weeklyMoney);
            
            document.getElementById('monthlyTime').textContent = monthlyTimeHours.toFixed(1) + ' hours';
            document.getElementById('monthlyMoney').textContent = formatCurrency(monthlyMoney);
            
            document.getElementById('annualTime').textContent = annualTimeHours.toFixed(1) + ' hours';
            document.getElementById('annualMoney').textContent = formatCurrency(annualMoney);
            
            // Update takeaways
            document.getElementById('takeSingleTime').textContent = singleRequestTimeHours.toFixed(1);
            document.getElementById('takeSingleMoney').textContent = formatCurrency(singleRequestMoney);
            document.getElementById('takeAnnualMoney').textContent = formatCurrency(annualMoney);
        }

        // Add event listeners to inputs
        document.getElementById('requestsPerWeek').addEventListener('input', calculateROI);
        document.getElementById('minutesPerRequest').addEventListener('input', calculateROI);
        document.getElementById('hourlyRate').addEventListener('input', calculateROI);
        
        // Initial calculation
        calculateROI();
    </script>
</body>
</html>
