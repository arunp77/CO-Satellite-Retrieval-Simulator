## Starting Point: The Inverse Problem

We have a **forward model** $F$ that tells us what the satellite *should* see for a given CO₂ scaling factor $\xi$:

$$\mathbf{y}_{\text{true}} = F(\xi)$$

But the satellite's measurement is contaminated by random noise $\boldsymbol{\epsilon}$:

$$\mathbf{y}_{\text{obs}} = F(\xi_{\text{true}}) + \boldsymbol{\epsilon}$$

We want to find $\hat{\xi}$ (our best guess of $\xi_{\text{true}}$) given only $\mathbf{y}_{\text{obs}}$.

---

## Step 1: The Simplest Approach — Least Squares

The most intuitive idea: find the $\xi$ whose forward model output $F(\xi)$ is **closest to the observation**. "Closest" means minimising the sum of squared differences:

$$J_{\text{data}}(\xi) = \sum_{k=1}^{n} \big(y_{\text{obs},k} - F_k(\xi)\big)^2$$

where $k$ indexes the $n$ spectral channels (wavenumbers). In vector notation:

$$J_{\text{data}}(\xi) = \big(\mathbf{y}_{\text{obs}} - F(\xi)\big)^T \big(\mathbf{y}_{\text{obs}} - F(\xi)\big) = \|\mathbf{y}_{\text{obs}} - F(\xi)\|^2$$

### Problem with plain least squares

Not all spectral channels are equally trustworthy. A channel with high noise ($\sigma_k = 5$) should count less than a channel with low noise ($\sigma_k = 0.1$). So we **weight** each channel by $1/\sigma_k^2$:

$$J_{\text{data}}(\xi) = \sum_{k=1}^{n} \frac{\big(y_{\text{obs},k} - F_k(\xi)\big)^2}{\sigma_k^2}$$

In our project, the noise is uniform across channels ($\sigma_k = \sigma_{\text{noise}}$ for all $k$), so this simplifies to:

$$J_{\text{data}}(\xi) = \frac{1}{\sigma_{\text{noise}}^2} \|\mathbf{y}_{\text{obs}} - F(\xi)\|^2$$

---

## Step 2: Why We Need a Prior (Regularisation)

Plain least squares has a subtle problem: **the inverse problem can be ill-conditioned**. Small amounts of noise in the observation can cause huge swings in the estimated $\xi$, because many different values of $\xi$ might produce nearly identical spectra (within the noise level).

The solution from Bayesian statistics: **add prior knowledge**. Before looking at any data, we have a reasonable guess: $\xi_a = 1.0$ (meaning our prior $XCO_2$ estimate is probably roughly correct). We're not very sure about this — we assign an uncertainty $\sigma_a = 0.10$ (10% uncertainty).

We add a **penalty** for straying too far from this prior:

$$J_{\text{prior}}(\xi) = \frac{(\xi - \xi_a)^2}{\sigma_a^2}$$

The total cost function is:

$$\boxed{J(\xi) = \underbrace{\frac{\|\mathbf{y}_{\text{obs}} - F(\xi)\|^2}{\sigma_{\text{noise}}^2}}_{\text{Fit the data}} + \underbrace{\frac{(\xi - \xi_a)^2}{\sigma_a^2}}_{\text{Stay near the prior}}}$$

The balance is automatic:
- **If data quality is high** (small $\sigma_{\text{noise}}$): the data term dominates → the answer trusts the measurement.
- **If data quality is low** (large $\sigma_{\text{noise}}$): the prior term dominates → the answer stays near the prior guess.

---

## Step 3: Linearising the Forward Model

The forward model $F(\xi)$ contains an exponential (Beer-Lambert law), making it non-linear. To find the minimum of $J(\xi)$ analytically, we approximate $F(\xi)$ as a straight line near the prior $\xi_a$:

$$F(\xi) \approx F(\xi_a) + \underbrace{\frac{\partial F}{\partial \xi}\bigg|_{\xi_a}}_{\mathbf{K}} \cdot (\xi - \xi_a)$$

Here $\mathbf{K}$ is the **Jacobian** — a vector of length $n$ telling us how much the radiance at each wavenumber changes when $\xi$ changes by a tiny amount. This is just the standard Taylor expansion (first-order approximation) of $F$ around $\xi_a$.

For the Beer-Lambert forward model $F(\xi) = I_\odot \cdot A_s \cdot \cos\theta_s \cdot e^{-M \sigma \cdot N_{\text{prior}} \cdot \xi}$, the derivative is:

$$K(\nu) = \frac{\partial I(\nu)}{\partial \xi} = -M \cdot \sigma(\nu) \cdot N_{\text{prior}} \cdot I(\nu)$$

(This is just the chain rule applied to the exponential.)

---

## Step 4: Deriving the Optimal Estimate (the Key Derivation)

Now substitute the linearised forward model into the cost function:

$$J(\xi) = \frac{1}{\sigma_{\text{noise}}^2} \big\|\mathbf{y}_{\text{obs}} - F(\xi_a) - \mathbf{K}(\xi - \xi_a)\big\|^2 + \frac{(\xi - \xi_a)^2}{\sigma_a^2}$$

Define the **residual** $\Delta\mathbf{y} = \mathbf{y}_{\text{obs}} - F(\xi_a)$ and a shift variable $\delta = \xi - \xi_a$:

$$J(\delta) = \frac{1}{\sigma_{\text{noise}}^2} \|\Delta\mathbf{y} - \mathbf{K}\delta\|^2 + \frac{\delta^2}{\sigma_a^2}$$

Now expand the squared norm (using $\|\mathbf{a}\|^2 = \mathbf{a}^T\mathbf{a}$):

$$J(\delta) = \frac{1}{\sigma_{\text{noise}}^2}\big(\Delta\mathbf{y}^T\Delta\mathbf{y} - 2\delta\,\mathbf{K}^T\Delta\mathbf{y} + \delta^2\,\mathbf{K}^T\mathbf{K}\big) + \frac{\delta^2}{\sigma_a^2}$$

To find the minimum, take the derivative with respect to $\delta$ and set it to zero:

$$\frac{dJ}{d\delta} = \frac{1}{\sigma_{\text{noise}}^2}\big(-2\,\mathbf{K}^T\Delta\mathbf{y} + 2\delta\,\mathbf{K}^T\mathbf{K}\big) + \frac{2\delta}{\sigma_a^2} = 0$$

Divide everything by 2:

$$\frac{-\mathbf{K}^T\Delta\mathbf{y}}{\sigma_{\text{noise}}^2} + \frac{\delta\,\mathbf{K}^T\mathbf{K}}{\sigma_{\text{noise}}^2} + \frac{\delta}{\sigma_a^2} = 0$$

Move the first term to the right side and factor out $\delta$:

$$\delta\left(\frac{\mathbf{K}^T\mathbf{K}}{\sigma_{\text{noise}}^2} + \frac{1}{\sigma_a^2}\right) = \frac{\mathbf{K}^T\Delta\mathbf{y}}{\sigma_{\text{noise}}^2}$$

Solve for $\delta$:

$$\delta = \frac{\mathbf{K}^T \Delta\mathbf{y} \;/\; \sigma_{\text{noise}}^2}{\mathbf{K}^T\mathbf{K} \;/\; \sigma_{\text{noise}}^2 + 1/\sigma_a^2}$$

Since $\hat{\xi} = \xi_a + \delta$:

$$\boxed{\hat{\xi} = \xi_a + \frac{\mathbf{K}^T S_\epsilon^{-1}\,(\mathbf{y}_{\text{obs}} - F(\xi_a))}{\mathbf{K}^T S_\epsilon^{-1}\,\mathbf{K} + S_a^{-1}}}$$

where $S_\epsilon^{-1} = 1/\sigma_{\text{noise}}^2$ and $S_a^{-1} = 1/\sigma_a^2$. **That's where this equation comes from** — it's simply setting the derivative of the cost function to zero and solving.

---

## Step 5: Deriving the Posterior Uncertainty

We want to know: *how confident are we in $\hat{\xi}$?* The **curvature** of $J(\xi)$ at the minimum tells us this. A sharply curved cost function means the minimum is well-defined (low uncertainty); a flat curve means many values of $\xi$ give similar cost (high uncertainty).

The curvature is the second derivative:

$$\frac{d^2J}{d\delta^2} = \frac{2\,\mathbf{K}^T\mathbf{K}}{\sigma_{\text{noise}}^2} + \frac{2}{\sigma_a^2}$$

For a quadratic function, the variance of the estimate is the inverse of half the second derivative:

$$\sigma_{\text{post}}^2 = \frac{1}{\mathbf{K}^T\mathbf{K}/\sigma_{\text{noise}}^2 + 1/\sigma_a^2}$$

Therefore:

$$\boxed{\sigma_{\text{post}} = \frac{1}{\sqrt{\mathbf{K}^T S_\epsilon^{-1}\,\mathbf{K} + S_a^{-1}}}}$$

**Physical intuition**: The posterior uncertainty is *always smaller* than the prior uncertainty $\sigma_a$, because adding data can only improve (or not change) our knowledge. The more informative the data ($\mathbf{K}^T S_\epsilon^{-1} \mathbf{K}$ is large), the smaller $\sigma_{\text{post}}$ becomes.

---

## Step 6: Deriving the Levenberg-Marquardt Iteration

The linear solution above works well when $F(\xi)$ is approximately linear near $\xi_a$. But for the real Beer-Lambert model, the exponential means the linear approximation breaks down if $\xi_{\text{true}}$ is far from $\xi_a$.

Solution: **iterate**. Start at $\xi_a$, take a step using the linear approximation, then re-linearise at the new point, and repeat.

At iteration $k$, we linearise around the current guess $\xi_k$:

$$F(\xi) \approx F(\xi_k) + \mathbf{K}_k(\xi - \xi_k)$$

Substituting into the cost function and minimising (following the same calculus as Step 4, but now relative to $\xi_k$ instead of $\xi_a$):

$$\frac{dJ}{d\xi}\bigg|_{\xi_k} = 0 \quad \Rightarrow \quad \Delta\xi = \frac{\mathbf{K}_k^T S_\epsilon^{-1}(\mathbf{y}_{\text{obs}} - F(\xi_k)) - S_a^{-1}(\xi_k - \xi_a)}{\mathbf{K}_k^T S_\epsilon^{-1}\mathbf{K}_k + S_a^{-1}}$$

Notice the **prior term** $-S_a^{-1}(\xi_k - \xi_a)$: it pulls $\xi$ back towards the prior when the current guess has drifted far from $\xi_a$.

### The Levenberg-Marquardt damping trick

Pure Gauss-Newton sometimes takes steps that are too large, causing the cost to *increase*. The Levenberg-Marquardt method adds a damping term $\gamma \cdot S_a^{-1}$ to the denominator:

$$\boxed{\Delta\xi = \frac{\mathbf{K}_k^T S_\epsilon^{-1}(\mathbf{y}_{\text{obs}} - F(\xi_k)) - S_a^{-1}(\xi_k - \xi_a)}{\mathbf{K}_k^T S_\epsilon^{-1}\mathbf{K}_k + S_a^{-1} + \gamma \cdot S_a^{-1}}}$$

- **Large $\gamma$**: Denominator is very large → $\Delta\xi$ is very small → cautious tiny steps (like gradient descent).
- **Small $\gamma$**: $\gamma$ contribution vanishes → same as the Gauss-Newton step (fast convergence near the solution).

The adaptive strategy in the code:
- If $J(\xi_{k+1}) < J(\xi_k)$: the step improved things → **accept** and reduce damping ($\gamma \leftarrow \gamma/3$).
- If $J(\xi_{k+1}) \geq J(\xi_k)$: the step made things worse → **reject** and increase damping ($\gamma \leftarrow 3\gamma$).

This guarantees the cost function never increases — the algorithm always converges toward a solution.

---

## Step 7: Converting $\hat{\xi}$ to $XCO_2$ in ppm

The scaling factor $\xi$ is defined such that:

$$N_{\text{col}}(\xi) = \xi \cdot N_{\text{col,prior}}$$

Since $N_{\text{col}}$ is proportional to $XCO_2$ (from the ideal gas law):

$$\widehat{XCO_2} = \hat{\xi} \cdot XCO_{2,\text{prior}}, \qquad \sigma_{XCO_2} = \sigma_{\text{post}} \cdot XCO_{2,\text{prior}}$$

If $\hat{\xi} = 1.035$ and $XCO_{2,\text{prior}} = 420$ ppm, then $\widehat{XCO_2} = 1.035 \times 420 = 434.7$ ppm.

---

## Summary of the Derivation Chain

```
Start:  We want ξ that makes F(ξ) match y_obs
  │
  ├─ Step 1:  Minimise ||y_obs - F(ξ)||²                    (least squares)
  ├─ Step 2:  Add prior penalty (ξ - ξ_a)²/σ_a²             (regularisation)
  ├─ Step 3:  Linearise F(ξ) ≈ F(ξ_a) + K·(ξ - ξ_a)        (Taylor expansion)
  ├─ Step 4:  Set dJ/dξ = 0, solve → closed-form ξ̂          (calculus)
  ├─ Step 5:  Curvature d²J/dξ² → posterior uncertainty      (error propagation)
  ├─ Step 6:  Iterate + add damping γ → Levenberg-Marquardt  (non-linear extension)
  └─ Step 7:  ξ̂ × XCO₂_prior → final answer in ppm          (unit conversion)
```

Every equation in [retrieval.py](cci:7://file:///home/arun/Documents/co2_measurements/src/retrieval.py:0:0-0:0) follows directly from this chain. There's no magic — it's just calculus applied to a carefully constructed cost function!