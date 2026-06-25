# Simulation Benchmarks

## Test Scenarios

### Scenario A: Single Agent Convergence
- **Setup**: 1 agent, 5 hierarchy levels, initial foam $\Phi_0 = 10$
- **Metric**: Time steps to $\Phi < 0.01$
- **Expected**: $t < 100$ steps

### Scenario B: Multi-Agent Swarm
- **Setup**: $N \in \{10, 100, 1000\}$ agents, random graph topology
- **Metric**: Consensus time, total foam reduction
- **Expected**: $O(\log N)$ consensus time

### Scenario C: Perturbation Recovery
- **Setup**: System at equilibrium, inject noise $\sigma = 0.5$ at $t = 500$
- **Metric**: Recovery time to 95% of baseline
- **Expected**: $t_{	ext{rec}} < 50$ steps

### Scenario D: Over-Hierarchy Collapse
- **Setup**: Gradually increase $L$ from 3 to 20
- **Metric**: $R_{	ext{hier}}$ vs $L$, critical threshold
- **Expected**: Critical $L^* pprox 7 \pm 2$

## Metrics

| Metric | Description | Target |
|--------|-------------|--------|
| $t_{	ext{conv}}$ | Convergence time | $< 100$ steps |
| $\Delta\Phi$ | Foam reduction | $> 99\%$ |
| $t_{	ext{rec}}$ | Recovery time | $< 50$ steps |
| $S$ | Scalability score | $> 0.8$ |

## Example Results

```
Scenario A: t_conv = 47 steps, dPhi = 99.7%
Scenario B (N=100): t_consensus = 12 steps, dPhi = 98.2%
Scenario C: t_rec = 23 steps
Scenario D: L* = 6 (R_hier = 4)
```

## Benchmark Suite

See `GRA-Validation-Suite` repository for full code and reproducible experiments.
