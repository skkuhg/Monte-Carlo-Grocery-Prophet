# 🤝 Contributing to Monte Carlo Grocery Prophet

Thank you for your interest in contributing! This document provides guidelines for contributing to the Monte Carlo Grocery Prophet project.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Process](#development-process)
- [Contribution Types](#contribution-types)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)
- [Pull Request Process](#pull-request-process)
- [Community](#community)

## 🤝 Code of Conduct

We are committed to providing a welcoming and inclusive environment for all contributors. Please read and follow our Code of Conduct:

### Our Pledge
- **Be respectful**: Treat all contributors with respect and kindness
- **Be inclusive**: Welcome contributors from all backgrounds and experience levels
- **Be constructive**: Provide helpful feedback and suggestions
- **Be collaborative**: Work together to improve the project

### Unacceptable Behavior
- Harassment, discrimination, or offensive language
- Personal attacks or trolling  
- Publishing private information without consent
- Any behavior that would be inappropriate in a professional setting

## 🚀 Getting Started

### Prerequisites
- Basic knowledge of JavaScript/Python
- Understanding of statistical concepts (helpful but not required)
- Git and GitHub experience

### Development Setup

1. **Fork the Repository**
   ```bash
   # Visit https://github.com/skkuhg/monte-grocery-prophet
   # Click "Fork" button
   ```

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/monte-grocery-prophet.git
   cd monte-grocery-prophet
   ```

3. **Set Up Development Environment**
   ```bash
   # For Python development
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   # or
   venv\Scripts\activate     # Windows
   
   pip install -r requirements.txt
   ```

4. **Create a Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/bug-description
   ```

## 🔄 Development Process

### Branch Naming Convention
- **Features**: `feature/description-of-feature`
- **Bug Fixes**: `fix/description-of-fix`
- **Documentation**: `docs/description-of-changes`
- **Refactoring**: `refactor/description-of-refactor`

### Commit Message Format
```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

**Examples:**
```
feat(simulation): add inflation adjustment feature

Add ability to apply inflation rates to price distributions
for sensitivity analysis scenarios.

Closes #123
```

```
fix(ui): correct chart rendering on mobile devices

- Fix responsive chart sizing issues
- Improve touch interactions for sliders
- Update chart legends for small screens

Fixes #456
```

## 🛠️ Contribution Types

### 1. Code Contributions

**High-Priority Areas:**
- **Performance Optimization**: Improve simulation speed
- **Mobile Responsiveness**: Better mobile UI/UX
- **Data Import**: Add CSV/Excel import functionality
- **Export Features**: PDF reports, data export
- **Advanced Analytics**: New risk metrics, correlation analysis

**Beginner-Friendly Tasks:**
- UI/UX improvements
- Documentation updates
- Bug fixes
- Test coverage improvements
- Translation/localization

### 2. Documentation Contributions

- **API Documentation**: Function/method documentation
- **Tutorials**: Step-by-step guides
- **Examples**: Real-world use cases
- **FAQ**: Common questions and answers
- **Video Tutorials**: Screen recordings or explanations

### 3. Testing Contributions

- **Unit Tests**: Individual function testing
- **Integration Tests**: End-to-end workflows
- **Performance Tests**: Benchmark simulations
- **Browser Compatibility**: Cross-browser testing
- **Accessibility Testing**: Screen reader compatibility

### 4. Design Contributions

- **UI/UX Improvements**: Better user interface
- **Accessibility**: WCAG compliance
- **Mobile Design**: Responsive layouts
- **Data Visualization**: Better charts and graphics
- **Branding**: Icons, logos, color schemes

## 📝 Coding Standards

### JavaScript Standards

**File Structure:**
```
monte-grocery-prophet/
├── js/
│   ├── core/
│   │   ├── simulation.js
│   │   ├── statistics.js
│   │   └── distributions.js
│   ├── ui/
│   │   ├── charts.js
│   │   ├── controls.js
│   │   └── results.js
│   └── utils/
│       ├── helpers.js
│       └── validation.js
```

**Code Style:**
```javascript
// Use descriptive variable names
const monthlySpendingResults = [];
const overspendProbability = 0.42;

// Function documentation
/**
 * Calculates Monte Carlo simulation for grocery spending
 * @param {Object} categories - Category spending parameters
 * @param {number} iterations - Number of simulation iterations
 * @param {number} budget - Monthly budget limit
 * @returns {Array<number>} Array of simulated monthly spending amounts
 */
function runMonteCarloSimulation(categories, iterations, budget) {
    // Implementation here
}

// Use consistent indentation (2 spaces)
if (condition) {
  doSomething();
  
  if (nestedCondition) {
    doNestedThing();
  }
}
```

### Python Standards (for Jupyter notebooks)

**PEP 8 Compliance:**
```python
# Import organization
import numpy as np
import pandas as pd
from scipy import stats

# Function definitions
def calculate_percentile(data: np.ndarray, percentile: float) -> float:
    """
    Calculate percentile value from data array.
    
    Args:
        data: Array of numerical values
        percentile: Percentile to calculate (0-100)
        
    Returns:
        Percentile value
    """
    return np.percentile(data, percentile)

# Class definitions
class MonteCarloSimulator:
    """Monte Carlo simulation engine for grocery budget analysis."""
    
    def __init__(self, categories: dict, budget: float):
        self.categories = categories
        self.budget = budget
        self.results = []
```

### HTML/CSS Standards

**Semantic HTML:**
```html
<!-- Use semantic elements -->
<main class="app-container">
  <header class="app-header">
    <h1>Monte Carlo Grocery Prophet</h1>
  </header>
  
  <section class="configuration-panel">
    <h2>Configuration</h2>
    <!-- Controls here -->
  </section>
  
  <section class="results-section">
    <h2>Results</h2>
    <!-- Results here -->
  </section>
</main>
```

**CSS Organization:**
```css
/* Use CSS custom properties */
:root {
  --primary-color: #667eea;
  --secondary-color: #764ba2;
  --accent-color: #f093fb;
  --text-color: #2c3e50;
  --background-color: #ffffff;
}

/* Mobile-first approach */
.app-container {
  padding: 1rem;
}

@media (min-width: 768px) {
  .app-container {
    padding: 2rem;
  }
}
```

## 🧪 Testing Guidelines

### Unit Testing

**JavaScript Testing (Jest):**
```javascript
// tests/simulation.test.js
describe('Monte Carlo Simulation', () => {
  test('should generate correct number of results', () => {
    const categories = mockCategories();
    const iterations = 1000;
    const results = runMonteCarloSimulation(categories, iterations, 600);
    
    expect(results).toHaveLength(iterations);
    expect(results.every(r => r > 0)).toBe(true);
  });
  
  test('should calculate percentiles correctly', () => {
    const data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    const p50 = calculatePercentile(data, 50);
    
    expect(p50).toBe(5.5);
  });
});
```

**Python Testing (pytest):**
```python
# tests/test_analysis.py
import pytest
import numpy as np
from monte_carlo_analysis import simulate_month, fit_distributions

def test_simulate_month():
    """Test monthly spending simulation."""
    categories = {
        'Produce': {'meanPrice': 2.0, 'stdPrice': 0.6, 'meanUnits': 2.5}
    }
    
    result = simulate_month(categories, seed=42)
    
    assert result > 0
    assert isinstance(result, float)

def test_fit_distributions():
    """Test distribution fitting functionality."""
    data = np.random.lognormal(mean=1.0, sigma=0.5, size=100)
    
    dist_name, params, aic = fit_distributions(data)
    
    assert dist_name in ['lognorm', 'gamma', 'norm', 'expon']
    assert len(params) > 0
    assert aic > 0
```

### Integration Testing

**End-to-End Testing:**
```javascript
// tests/e2e/simulation-flow.test.js
describe('Complete Simulation Flow', () => {
  test('should complete full analysis workflow', () => {
    // Load application
    cy.visit('/grocery_budget_app.html');
    
    // Set configuration
    cy.get('#budget').clear().type('600');
    cy.get('#iterations').invoke('val', 5000);
    
    // Run simulation
    cy.contains('Run Monte Carlo Simulation').click();
    
    // Verify results
    cy.get('#results-section').should('be.visible');
    cy.get('#overspend-prob').should('contain.text', '%');
    cy.get('#expected-spend').should('contain.text', '$');
  });
});
```

## 📚 Documentation

### Code Documentation

**Function Documentation:**
```javascript
/**
 * Fits statistical distributions to price data and selects best fit
 * 
 * @param {number[]} data - Array of price values
 * @param {string} categoryName - Name of grocery category
 * @returns {Object} Object containing distribution name, parameters, and AIC
 * @example
 * 
 * const data = [2.1, 2.5, 1.9, 2.8, 2.3];
 * const result = fitDistributions(data, 'Produce');
 * // Returns: { name: 'lognorm', params: [0.1, 0.2], aic: 15.3 }
 */
function fitDistributions(data, categoryName) {
    // Implementation
}
```

### README Updates

When adding features, update relevant sections:
- Features list
- Installation instructions  
- Usage examples
- API documentation

### Changelog

Follow [Keep a Changelog](https://keepachangelog.com/) format:

```markdown
## [Unreleased]

### Added
- New sensitivity analysis heatmap visualization
- CSV data import functionality

### Changed
- Improved mobile responsive design
- Updated chart color scheme for better accessibility

### Fixed
- Fixed chart rendering issue on Safari browsers
- Corrected percentile calculations for edge cases

### Removed
- Deprecated old chart library dependency
```

## 🔄 Pull Request Process

### Before Submitting

1. **Test Your Changes**
   ```bash
   # Run all tests
   npm test
   # or
   pytest
   
   # Test in multiple browsers
   # Check mobile responsiveness
   ```

2. **Code Review Checklist**
   - [ ] Code follows project style guidelines
   - [ ] All tests pass
   - [ ] Documentation updated
   - [ ] No console errors or warnings
   - [ ] Accessible design (WCAG guidelines)
   - [ ] Mobile responsive

3. **Update Documentation**
   - Update README.md if needed
   - Add/update code comments
   - Update CHANGELOG.md

### Pull Request Template

```markdown
## Description
Brief description of the changes and why they're needed.

## Type of Change
- [ ] Bug fix (non-breaking change that fixes an issue)
- [ ] New feature (non-breaking change that adds functionality)
- [ ] Breaking change (fix or feature that causes existing functionality to not work as expected)
- [ ] Documentation update

## Testing
Describe the tests you ran and how to reproduce them.

## Screenshots
If applicable, add screenshots to help explain your changes.

## Checklist
- [ ] My code follows the project's style guidelines
- [ ] I have performed a self-review of my code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes
```

### Review Process

1. **Automated Checks**: All CI/CD checks must pass
2. **Code Review**: At least one maintainer review required
3. **Testing**: Manual testing for UI changes
4. **Documentation Review**: Ensure docs are updated
5. **Approval**: Maintainer approval required for merge

## 👥 Community

### Getting Help

- **GitHub Issues**: Technical problems and bug reports
- **GitHub Discussions**: General questions and feature ideas
- **Documentation**: Check existing docs first
- **Examples**: Look at usage examples for guidance

### Communication Channels

- **Issues**: Bug reports and feature requests
- **Discussions**: General questions and ideas
- **Pull Requests**: Code contributions and reviews
- **Wiki**: Community knowledge base

### Recognition

Contributors will be recognized in:
- README.md contributors section
- Release notes for significant contributions
- GitHub contributor graphs and statistics

### Mentorship

**For New Contributors:**
- Look for issues labeled `good first issue`
- Ask questions in discussions
- Start with documentation or small bug fixes
- Pair programming sessions available upon request

**For Experienced Contributors:**
- Help review pull requests
- Mentor new contributors
- Lead feature development
- Help with architectural decisions

## 📧 Contact

For questions about contributing, please:

1. Check existing documentation
2. Search GitHub issues and discussions
3. Create a new discussion for general questions
4. Create an issue for specific bugs or feature requests

Thank you for contributing to Monte Carlo Grocery Prophet! Your efforts help make grocery budgeting more accessible and data-driven for everyone. 🛒📊

---

*This contributing guide is a living document. Please suggest improvements through issues or pull requests.*