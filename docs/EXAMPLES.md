# 💡 Usage Examples

This guide provides practical examples of using Monte Carlo Grocery Prophet for different scenarios and use cases.

## 🚀 Quick Start Examples

### Example 1: Basic Budget Analysis
```html
<!-- Open grocery_budget_app.html in your browser -->
<!-- Set your parameters: -->
Budget: $600
Iterations: 5000
Categories: Default values

<!-- Click "Run Monte Carlo Simulation" -->
<!-- Results: Overspend probability and risk percentiles -->
```

**Sample Output:**
```
📊 Risk Analysis Results:

Overspend Probability: 42.3%
Expected Monthly Spend: $587.45
95% VaR: $742.89
Recommended Buffer: $55.23

Interpretation: 42% chance of exceeding $600 budget, 
with worst-case spending around $743.
```

## 🎯 Scenario-Based Examples

### Scenario 1: Budget-Conscious Family
**Profile:** Family of 4, tight budget, price-sensitive shopping

**Configuration:**
- Budget: $400
- Focus on: Produce, Dairy, Bakery
- Reduce: Meat, Snacks spending

**Strategy:**
```javascript
// Adjust categories for budget-conscious shopping
categories = {
    'Produce': { meanPrice: 1.5, stdPrice: 0.4, meanUnits: 3.0 },
    'Dairy': { meanPrice: 3.5, stdPrice: 1.0, meanUnits: 2.8 },
    'Meat': { meanPrice: 6.0, stdPrice: 1.5, meanUnits: 1.5 },  // Reduced
    'Snacks': { meanPrice: 2.0, stdPrice: 0.5, meanUnits: 1.0 }, // Reduced
    'Beverages': { meanPrice: 2.0, stdPrice: 0.5, meanUnits: 2.0 },
    'Bakery': { meanPrice: 2.5, stdPrice: 0.7, meanUnits: 2.5 }
};
```

**Expected Results:**
- Lower overspend probability (~25%)
- More predictable spending patterns
- Focus on essential categories

### Scenario 2: Premium Shopping Lifestyle
**Profile:** High-income household, organic/premium preferences

**Configuration:**
- Budget: $1,000
- Higher prices across all categories
- Emphasis on quality over quantity

**Strategy:**
```javascript
categories = {
    'Produce': { meanPrice: 3.5, stdPrice: 1.2, meanUnits: 2.8 }, // Organic
    'Dairy': { meanPrice: 6.0, stdPrice: 2.0, meanUnits: 2.2 },  // Premium
    'Meat': { meanPrice: 15.0, stdPrice: 4.0, meanUnits: 2.0 },  // Grass-fed
    'Snacks': { meanPrice: 5.0, stdPrice: 1.5, meanUnits: 2.0 }, // Artisanal
    'Beverages': { meanPrice: 4.5, stdPrice: 1.2, meanUnits: 2.2 },
    'Bakery': { meanPrice: 6.0, stdPrice: 2.0, meanUnits: 2.0 }  // Artisan
};
```

**Expected Results:**
- Higher absolute spending but lower budget risk
- More volatile due to premium price variations
- Focus on risk management strategies

### Scenario 3: Inflation Impact Analysis
**Profile:** Standard household analyzing inflation effects

**Setup:**
```javascript
// Base scenario
runSimulation(budget: 600, inflation: 0%);

// Inflation scenarios
[2%, 5%, 10%, 15%].forEach(inflation => {
    adjustedResults = baseResults * (1 + inflation/100);
    analyzeRisk(adjustedResults, budget);
});
```

**Analysis Framework:**
```
Inflation Rate | Overspend Risk | Recommended Action
0%            | 35%           | Maintain current budget
2%            | 41%           | Monitor closely
5%            | 52%           | Increase budget by 5-8%
10%           | 68%           | Increase budget by 12-15%
15%           | 78%           | Major budget revision needed
```

## 📊 Advanced Usage Patterns

### Pattern 1: Seasonal Analysis

**Holiday Season (November-December):**
```javascript
// Increase spending in categories
holidayMultipliers = {
    'Produce': 1.2,  // More fresh ingredients
    'Meat': 1.5,     // Holiday roasts
    'Bakery': 1.8,   // Holiday desserts
    'Beverages': 1.3, // Entertainment
    'Snacks': 1.4,   // Party foods
    'Dairy': 1.1     // Baking supplies
};

Object.keys(categories).forEach(cat => {
    categories[cat].meanPrice *= holidayMultipliers[cat];
});
```

**Summer Season (June-August):**
```javascript
// Adjust for seasonal patterns
summerAdjustments = {
    'Produce': { meanPrice: -0.3, meanUnits: +0.5 }, // Cheaper, more fresh
    'Beverages': { meanPrice: +0.2, meanUnits: +0.8 }, // More drinks
    'Meat': { meanPrice: +0.5, meanUnits: +0.3 }, // BBQ season
    'Dairy': { meanPrice: 0, meanUnits: -0.2 } // Less baking
};
```

### Pattern 2: Category Deep-Dive Analysis

**Focus on High-Impact Category:**
```javascript
// Analyze meat category sensitivity
meatPriceScenarios = [6, 8, 10, 12, 15]; // $/unit

results = meatPriceScenarios.map(price => {
    tempCategories = {...categories};
    tempCategories.Meat.meanPrice = price;
    return runMonteCarloSimulation(tempCategories);
});

// Identify price threshold where risk becomes unacceptable
```

### Pattern 3: Budget Optimization

**Find Optimal Budget Level:**
```javascript
function findOptimalBudget(targetRisk = 0.25) {
    let budget = 400;
    let risk = 1.0;
    
    while (risk > targetRisk && budget < 1000) {
        simulationResults = runSimulation();
        risk = calculateOverspendRisk(simulationResults, budget);
        budget += 25;
    }
    
    return budget - 25; // Return last acceptable budget
}

// Usage: Find budget for 25% risk tolerance
optimalBudget = findOptimalBudget(0.25);
```

## 🔧 Customization Examples

### Custom Category Addition

**Adding "Household Items" Category:**
```javascript
categories['Household'] = {
    meanPrice: 4.5,
    stdPrice: 1.8,
    meanUnits: 1.8,
    color: '#607D8B'
};

// Update UI
updateCategoryGrid();
```

### Custom Risk Metrics

**Add "Budget Stress Score":**
```javascript
function calculateStressScore(results, budget) {
    const exceededAmount = results
        .filter(x => x > budget)
        .map(x => x - budget);
    
    const avgExceedance = exceededAmount.reduce((a,b) => a+b, 0) / exceededAmount.length;
    const maxExceedance = Math.max(...exceededAmount);
    
    // Stress score: 0-100 (higher = more stressful)
    return Math.min(100, (avgExceedance + maxExceedance) / budget * 100);
}
```

### Custom Visualization

**Add Risk Timeline Chart:**
```javascript
function createRiskTimelineChart(results) {
    // Simulate 12 months of risk evolution
    const monthlyRisks = Array.from({length: 12}, (_, i) => {
        const monthlyResults = results.slice(i * 100, (i + 1) * 100);
        return calculateOverspendRisk(monthlyResults, budget);
    });
    
    // Create Chart.js line chart
    new Chart(ctx, {
        type: 'line',
        data: {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 
                    'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            datasets: [{
                label: 'Monthly Risk (%)',
                data: monthlyRisks,
                borderColor: '#FF6384',
                tension: 0.1
            }]
        }
    });
}
```

## 🎯 Use Case Examples

### Use Case 1: Personal Finance Planning
**Goal:** Set realistic monthly grocery budget

**Process:**
1. Gather 3-6 months of receipt data
2. Run analysis with current spending patterns
3. Identify comfortable risk level (e.g., 20% overspend risk)
4. Adjust budget to meet risk target
5. Implement weekly tracking system

### Use Case 2: Family Budget Meeting
**Goal:** Involve family in budget-conscious decisions

**Approach:**
```
1. Show current risk analysis results
2. Demonstrate impact of different shopping strategies:
   - Generic vs. brand name products
   - Meal planning vs. impulse buying
   - Bulk buying vs. regular purchases
3. Set family savings goals with visual feedback
4. Monthly review sessions with updated analysis
```

### Use Case 3: Financial Advisory Services
**Goal:** Help clients with grocery budget optimization

**Framework:**
```
1. Client Data Collection:
   - Income level and financial goals
   - Family size and dietary requirements  
   - Current spending patterns
   
2. Risk Assessment:
   - Conservative clients: 15% overspend risk
   - Moderate clients: 25% overspend risk
   - Aggressive clients: 35% overspend risk
   
3. Recommendation Development:
   - Budget allocation suggestions
   - Shopping strategy optimization
   - Emergency fund calculations
```

### Use Case 4: Research & Analysis
**Goal:** Study consumer spending patterns

**Research Questions:**
- How does price volatility affect spending behavior?
- What's the impact of inflation on grocery budgets?
- Which categories drive the most budget uncertainty?

**Methodology:**
```python
# Pseudo-code for research analysis
def research_analysis():
    households = load_household_data()
    
    for household in households:
        results = run_monte_carlo_analysis(household.data)
        
        # Collect metrics
        metrics = {
            'income_level': household.income,
            'family_size': household.size,
            'overspend_risk': calculate_risk(results),
            'price_sensitivity': calculate_sensitivity(results),
            'category_allocation': analyze_categories(results)
        }
        
        research_dataset.append(metrics)
    
    # Statistical analysis
    correlations = analyze_correlations(research_dataset)
    regressions = fit_regression_models(research_dataset)
```

## 📈 Performance Optimization Tips

### Tip 1: Simulation Size Selection
```javascript
// Choose iteration count based on precision needs:
const precisionMap = {
    'quick_estimate': 1000,    // ±3% accuracy
    'standard_analysis': 5000,  // ±1.5% accuracy  
    'high_precision': 10000,   // ±1% accuracy
    'research_grade': 50000    // ±0.5% accuracy
};
```

### Tip 2: Category Granularity
```javascript
// Balance detail vs. complexity
const categoryLevels = {
    'basic': ['Food', 'Beverages'],
    'standard': ['Produce', 'Dairy', 'Meat', 'Snacks', 'Beverages', 'Bakery'],
    'detailed': ['Fruits', 'Vegetables', 'Milk', 'Cheese', 'Beef', 'Poultry', 
                'Chips', 'Cookies', 'Soda', 'Juice', 'Bread', 'Pastries']
};
```

### Tip 3: Data Quality Optimization
```javascript
// Pre-processing for better results
function optimizeData(rawData) {
    return rawData
        .filter(removeOutliers)
        .map(normalizeInflation)
        .groupBy(consolidateCategories)
        .validate(dataQualityChecks);
}
```

---

*These examples demonstrate the flexibility and power of Monte Carlo Grocery Prophet. Adapt them to your specific needs and use cases.*