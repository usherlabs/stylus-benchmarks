# Solidity vs Stylus Execution Cost Comparison

## ERC Gas Cost Comparison Table
**ERC20 Functions (Solidity Implementation: 7927)**
| Contract Function | Solidity (Gas) | Stylus WASM Opt & Cached | Stylus Cached | Stylus Not Cached |
|------------------|----------------|-------------------------|---------------|-------------------|
| `totalSupply()` | 45,274 | 4,753 (-89.5%) | 5,991 (-86.8%) | 24,821 (-45.2%) |
| `allowance(address,address)` | 32,599 | 6,786 (-79.2%) | 8,033 (-75.4%) | 26,875 (-17.6%) |
| `approve(address,uint256)` | 7,692 | 28,540 (+271.0%) | 29,840 (+287.9%) | 48,670 (+532.7%) |
| `transferFromToOwner` | 37,744 | 22,254 (-41.0%) | 23,589 (-37.5%) | 42,431 (+12.4%) |
| `transferFromToNonOwner` | 28,152 | 22,254 (-20.9%) | 23,589 (-16.2%) | 42,431 (+50.7%) |
| `transferToNonOwner` | 20,666 | 36,393 (+76.2%) | 37,707 (+82.5%) | 56,537 (+173.8%) |

**ERC721 Functions (OpenZeppelin Implementation)**

| Contract Function | Solidity (Gas) | Stylus WASM Opt & Cached | Stylus Cached | Stylus Not Cached |
|------------------|----------------|-------------------------|---------------|-------------------|
| `mint()` | 74,572 | 133,318 (+78.7%) | 135,223 (+81.3%) | 158,335 (+112.3%) |
| `burn()` | 18,518 | 38,008 (+105.2%) | 39,584 (+113.7%) | 58,073 (+213.5%) |
| `transferFrom()` | 28,930 | 58,377 (+101.8%) | 60,328 (+108.6%) | 83,440 (+188.5%) |
| `ownerOf()` | 7,762 | 5,434 (-30.0%) | 7,243 (-6.7%) | 30,355 (+291.2%) |
| `approve(address,uint256)` | 35,163 | 30,716 (-12.6%) | 32,562 (-7.4%) | 55,674 (+58.3%) |

**ERC1155 Functions (OpenZeppelin Implementation)** 
| Contract Function | Solidity (Gas) | Stylus WASM Opt & Cached | Stylus Cached | Stylus Not Cached |
|------------------|----------------|-------------------------|---------------|-------------------|
| `mint()` | 33,906 | 32,341 (-4.6%) | 34,491 (+1.7%) | 58,022 (+71.1%) |
| `mintBatch()` | 35,443 | 90,740 (+156.0%) | 93,026 (+162.5%) | 116,557 (+228.9%) |
| `safeTransferFrom()` | 38,038 | 42,610 (+12.0%) | 44,800 (+17.8%) | 68,331 (+79.7%) |
| `safeBatchTransferFrom()` | 39,850 | 103,712 (+160.2%) | 106,141 (+166.2%) | 129,672 (+225.3%) |


## ERC Token Function Observations

• **Stylus excels at read operations**: Functions like `totalSupply()`, `allowance()`, `ownerOf()` show up to 89.5% gas savings compared to Solidity

• **Solidity maintains advantages for write operations**: Functions like `approve()` and batch transfers perform better in Solidity due to EVM's optimized state management

---

## Mathematical Computation Comparison

### Straight Line Equation Implementation

Both contracts implement the same mathematical function: `y = mx + b` with 50 iterations.

**Code Functionality:**
```solidity
// Solidity Implementation
function run50Loops() public returns (uint256) {
    uint256 gasStart = gasleft();
    for (uint256 i = 0; i < 50; i++) {
        int256 x = int256(i);
        int256 y = calculateY(x); // y = (slope * x) + yIntercept
    }
    completed = true;
    uint256 gasUsed = gasStart - gasleft();
    totalGasUsed = gasUsed;
    return gasUsed;
}
```

```rust
// Stylus Implementation  
pub fn run_50_loops(&mut self) -> bool {
    for i in 0..50 {
        let x = I256::try_from(i).unwrap();
        let _y = self.calculate_y(x); // y = (slope * x) + y_intercept
    }
    self.completed.set(true);
    true
}
```

### Gas Cost Analysis

| Contract Type | Gas Used | Gas per Iteration | Performance Ratio |
|---------------|----------|-------------------|-------------------|
| **Stylus** | 62,982 | ~1,260 | 1.0x (baseline) |
| **Solidity** | 111,443 | ~2,229 | 1.77x slower |

### Mathematical Computation Observations

• **Stylus shows 43.5% gas efficiency improvement** for mathematical computations due to WASM compilation and reduced EVM interpretation overhead

• **Solidity has higher computational costs** due to stack-based architecture and EVM interpretation layer, making it less suitable for intensive mathematical operations


## Conclusion

**Stylus excels at computational tasks** (43.5% gas savings for math operations, up to 89.5% for read functions) while **Solidity maintains advantages for state management operations** (write operations and batch processing). This makes Stylus ideal for DeFi protocols requiring frequent calculations and read operations, while Solidity remains better for complex state transitions and cross-chain compatibility. 