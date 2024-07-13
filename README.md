
# Email Spam Filtering using Fuzzy Logic
# Overview
This program determines the likelihood of an email being spam based on keyword frequency, number of links, and sender reputation using fuzzy logic.

# Requirements
Python 3.x <br>
NumPy<br>
scikit-fuzzy<br>

# Installation
Install the required libraries with:

```bash 
pip install numpy scikit-fuzzy
```
# Inputs
keyword_freq (0 to 10)<br>
num_links (0 to 10)<br>
sender_reputation (0 to 10)<br>
# Output
spam_likelihood (0 to 100%)<br>

# Fuzzy Sets -

# Keyword Frequency
Low: [0, 0, 5]<br>
Medium: [0, 5, 10]<br>
High: [5, 10, 10]<br>

# Number of Links
Few: [0, 0, 5]<br>
Moderate: [0, 5, 10]<br>
Many: [5, 10, 10]<br>

# Sender Reputation
Poor: [0, 0, 5]<br>
Average: [0, 5, 10]<br>
Good: [5, 10, 10]<br>

# Spam Likelihood
Low: [0, 0, 50]<br>
Medium: [0, 50, 100]<br>
High: [50, 100, 100]<br>

# Rules
1.High keyword frequency & many links & poor reputation → High spam likelihood<br>
2.Medium keyword frequency & moderate links & average reputation → Medium spam likelihood<br>
3.Low keyword frequency & few links & good reputation → Low spam likelihood<br>

# Usage
```python
import numpy as np
import skfuzzy as fuzz
from skfuzzy import control as ctrl

# Define fuzzy variables
keyword_freq = ctrl.Antecedent(np.arange(0, 11, 1), 'keyword_freq')
num_links = ctrl.Antecedent(np.arange(0, 11, 1), 'num_links')
sender_reputation = ctrl.Antecedent(np.arange(0, 11, 1), 'sender_reputation')
spam_likelihood = ctrl.Consequent(np.arange(0, 101, 1), 'spam_likelihood')

# Define fuzzy sets
keyword_freq.automf(3)
num_links.automf(3)
sender_reputation.automf(3)
spam_likelihood.automf(3)

# Define rules
rule1 = ctrl.Rule(keyword_freq['high'] & num_links['many'] & sender_reputation['poor'], spam_likelihood['high'])
rule2 = ctrl.Rule(keyword_freq['average'] & num_links['average'] & sender_reputation['average'], spam_likelihood['medium'])
rule3 = ctrl.Rule(keyword_freq['low'] & num_links['few'] & sender_reputation['good'], spam_likelihood['low'])

# Control system
spam_control = ctrl.ControlSystem([rule1, rule2, rule3])
spam_simulation = ctrl.ControlSystemSimulation(spam_control)

# Input values
spam_simulation.input['keyword_freq'] = 6
spam_simulation.input['num_links'] = 8
spam_simulation.input['sender_reputation'] = 3

# Compute result
spam_simulation.compute()
spam_score = spam_simulation.output['spam_likelihood']

print(f"Spam Likelihood: {spam_score}%")
spam_likelihood.view(sim=spam_simulation
```
# Summary
Python 3.x: Language interpreter.<br>
NumPy: For numerical operations and array handling.<br>
scikit-fuzzy: For fuzzy logic operations.<br>
Matplotlib (optional): For plotting and visualization.<br>
