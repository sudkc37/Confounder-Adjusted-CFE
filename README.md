

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
                            <li>Generating DAGs using Hill Climbing search with BIC scoring.</li>
                            <li>Identifying variables that influence both treatment and outcome.</li>
                            <li>Imposing constraints to ensure causal relationships with outcome variables.</li>
                        </ul>
                    <div class="step">
                        <h3>2. Confounder Filtration Method (CFM)</h3>
                        <p>Once confounders are identified from the DAG, we filter them out during model training to prevent bias:</p>
                        <ul>
                            <li><strong>Create Binary Mask:</strong> Generate a mask matrix M where confounder positions are set to 0, and all other features are set to 1.</li>
                            <li><strong>Apply Element-wise Multiplication:</strong> Multiply input data X with mask M to zero out confounding features.</li>
                            <li><strong>Train Neural Network:</strong> Train the model on masked data X_masked, ensuring confounders don't influence predictions.</li>
                        </ul>
                       </div>

  <div class="step">
                        <h3>3. Counterfactual Generation with Adjusted DICE</h3>
                        <p>We generate diverse counterfactual explanations using the confounder-free model through a multi-objective optimization:</p>
                        <ul>
                            <li><strong>yloss term:</strong> Ensures counterfactuals achieve the desired prediction outcome (e.g., loan approval).</li>
                            <li><strong>dist term:</strong> Minimizes changes from the original instance - finding the smallest adjustments needed.</li>
                            <li><strong>dpp term:</strong> Maintains diversity among counterfactuals using Determinantal Point Process, giving multiple actionable options.</li>
                            <li><strong>λ weights:</strong> Balance between prediction accuracy, proximity to original, and diversity.</li>
                        </ul>
                        
      

  <div class="section">
                <h2>Performance Improvements</h2>
                
      

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
