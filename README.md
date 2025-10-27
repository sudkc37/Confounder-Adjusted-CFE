Counterfactual Explanation for Tabular Dataset.

I am using Bayesian network to get the DAGs to identify the confounder before training and then masking them to get confounder free training model for CounterFactual Explaination Model.



 <header>
        <div class="container">
            <h1>Confounder-Adjusted Counterfactual Explanations for Tabular Data</h1>
            <p class="subtitle">A novel approach to generating bias-reduced counterfactual explanations by identifying and adjusting for confounding variables using Bayesian networks and DAG analysis.</p>
        </div>
    </header>

  <div class="container">
        <div class="content">
            <div class="section">
                <h2>Overview</h2>
                <p>This project extends existing counterfactual explanation methods (Wachter et al., DICE) by incorporating a confounder identification and filtration technique. By adjusting for confounding variables before model training this model achieve improved prediction accuracy and more reliable counterfactual explanations.</p>
            </div>

   <div class="section">
                <h2>Key Features</h2>
                <div class="feature-grid">
                    <div class="feature-card">
                      
**Confounder Identification :** Uses Bayesian networks with Hill Climbing search to generate Directed Acyclic Graphs (DAGs) and identify confounding variables.
         
**Bias Reduction :** Masks confounders during training to reduce bias in both predictions and counterfactual generation.

**Enhanced DICE :** Integrates confounder-free models into the DICE optimization framework.
                      
**Improved Performance :** Achieves 90.43% test accuracy (up from 85.51%) with reduced MSE loss.
                        

   <div class="section">
                <h2>Methodology</h2>
                
   <div class="methodology-steps">
                    <div class="step">
                        <h3>1. Confounder Identification via Bayesian Networks</h3>
                        <p>The system identifies confounding variables by:</p>
                        <ul>
                            <li>Generating DAGs using Hill Climbing search with BIC scoring</li>
                            <li>Identifying variables that influence both treatment and outcome</li>
                            <li>Imposing constraints to ensure causal relationships with outcome variables</li>
                        </ul>
                    </div>

 <div class="step">
                        <h3>2. Confounder Filtration Method (CFM)</h3>
                        <p>During training, identified confounders are masked:</p>
                        <div class="code-block">X_masked = X ⊙ M</div>
                        <p>Where M is a binary mask matrix that zeros out confounder features.</p>
                    </div>

  <div class="step">
                        <h3>3. Counterfactual Generation</h3>
                        <p>Extends DICE optimization to use confounder-free models:</p>
                        <div class="code-block">C(x) = arg min [yloss(f(C_i), y) + dist(C_i, x) - λ * dpp(C_1,...,C_n)]</div>
                    </div>
                </div>
            </div>

  <div class="section">
                <h2>Performance Improvements</h2>
                <div class="highlight">
                    <div class="stats">
                        <div class="stat-card">
                            <div class="stat-number">+4.92%</div>
                            <div class="stat-label">Test Accuracy Improvement</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">90.43%</div>
                            <div class="stat-label">Final Test Accuracy</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-number">-13.8%</div>
                            <div class="stat-label">MSE Loss Reduction</div>
                        </div>
                    </div>
                </div>

  <table>
                    <thead>
                        <tr>
                            <th>Metric</th>
                            <th>Before Adjustment</th>
                            <th>After Adjustment</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>Test Accuracy</strong></td>
                            <td>85.51%</td>
                            <td><strong>90.43%</strong></td>
                        </tr>
                        <tr>
                            <td><strong>Training Accuracy</strong></td>
                            <td>91.8%</td>
                            <td><strong>92.87%</strong></td>
                        </tr>
                        <tr>
                            <td><strong>Loss (MSE)</strong></td>
                            <td>0.29</td>
                            <td><strong>0.25</strong></td>
                        </tr>
                    </tbody>
                </table>
            </div>

 <div class="section">
                <h2>Model Properties Comparison</h2>
                <table>
                    <thead>
                        <tr>
                            <th>Property</th>
                            <th>Wachter et al.</th>
                            <th>DICE</th>
                            <th>Adjusted-DICE</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>Actionability</strong></td>
                            <td><span class="checkmark">✓</span></td>
                            <td><span class="checkmark">✓</span></td>
                            <td><span class="checkmark">✓</span></td>
                        </tr>
                        <tr>
                            <td><strong>Sparsity</strong></td>
                            <td><span class="crossmark">×</span></td>
                            <td><span class="checkmark">✓</span></td>
                            <td><span class="checkmark">✓</span></td>
                        </tr>
                        <tr>
                            <td><strong>Causality</strong></td>
                            <td><span class="checkmark">✓</span></td>
                            <td><span class="checkmark">✓</span></td>
                            <td><span class="checkmark">✓</span></td>
                        </tr>
                        <tr>
                            <td><strong>Data Manifold</strong></td>
                            <td><span class="crossmark">×</span></td>
                            <td><span class="checkmark">✓</span></td>
                            <td><span class="checkmark">✓</span></td>
                        </tr>
                        <tr>
                            <td><strong>Low Time Complexity</strong></td>
                            <td><span class="crossmark">×</span></td>
                            <td><span class="checkmark">✓</span></td>
                            <td><span class="checkmark">✓</span></td>
                        </tr>
                        <tr>
                            <td><strong>Model Access</strong></td>
                            <td>Model-agnostic</td>
                            <td>Model-agnostic</td>
                            <td>Model-agnostic</td>
                        </tr>
                        <tr>
                            <td><strong>Confounder Adjustment</strong></td>
                            <td><span class="crossmark">×</span></td>
                            <td><span class="crossmark">×</span></td>
                            <td><span class="checkmark">✓</span></td>
                        </tr>
                    </tbody>
                </table>
            </div>

  <div class="section">
                <h2>GitHub Repository</h2>
                <div class="highlight">
                    <p style="font-size: 1.1em;">Access the complete source code, documentation, and examples:</p>
                    <p style="margin-top: 15px;"><strong>🔗 <a href="https://github.com/sudkc37" style="color: #667eea; text-decoration: none; font-weight: 600;">github.com/sudkc37</a></strong></p>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
