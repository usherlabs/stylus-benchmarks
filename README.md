# Solidity vs Stylus Performance Benchmarking

Performance benchmarks comparing Solidity and Stylus smart contracts across different optimization levels and use cases.

## Benchmarks

- **ERC20 Functions**: Standard token operations (totalSupply, allowance, approve, transfer) tested across WASM optimized, cached, and non-cached scenarios
- **Mathematical Computations**: Straight line equation (`y = mx + b`) with 50 iterations to measure computational efficiency. This benchmark tests basic arithmetic operations, loop performance, and function call overhead in both languages.

## Files

- **`solidity_vs_stylus_comparison.md`**: Complete gas cost analysis with detailed observations and conclusions
- **`stylus_vs_solidity_charts.html`**: Interactive bar charts and performance visualizations with hover effects

## Viewing Charts

To view the interactive charts:
1. Enable GitHub Pages in your repository settings
2. Navigate to `https://usherlabs.github.io/stylus-benchmarks/stylus_vs_solidity_charts.html`
3. Or download the HTML file and open it locally in your browser

