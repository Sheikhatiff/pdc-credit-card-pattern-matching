# Credit Card Pattern Matching & Validation

## 📋 Project Overview
A high-performance hybrid computing solution that generates and validates 10 million credit card numbers using CUDA (GPU acceleration) and OpenMP (CPU parallelism). The system performs pattern matching (VISA/MasterCard) and Luhn algorithm validation with exceptional throughput.

## 🚀 Key Features
- **Hybrid Architecture**: CUDA + OpenMP implementation
- **Massive Scale**: Processes 10 million credit cards
- **Real-time Validation**: Pattern matching + Luhn algorithm check
- **High Throughput**: 1.62 million cards/second processing speed
- **Detailed Analytics**: Comprehensive performance metrics and results

## 🏗️ System Architecture
```
Input Generation (OpenMP) → GPU Validation (CUDA) → Results Aggregation (OpenMP)
```

## ⚙️ Technical Specifications
- **GPU**: NVIDIA Tesla T4 (2,560 CUDA cores)
- **CPU Parallelism**: OpenMP multi-threading
- **Validation Methods**:
  - Pattern matching (VISA: starts with 4, MasterCard: 51-55)
  - Luhn algorithm checksum validation
- **Data Size**: 10 million credit cards (16-digit each)

## 📊 Performance Results
| Metric | Value |
|--------|-------|
| Total Cards Processed | 10,000,000 |
| Valid Cards | ~1,000,000 (10.01%) |
| Invalid Cards | ~9,000,000 |
| Total Execution Time | 6.1681 seconds |
| Generation Time (OpenMP) | 5.9959 seconds |
| Validation Time (CUDA) | 0.1722 seconds |
| CUDA Kernel Time | 0.0041 seconds |
| Throughput | 1.62 million cards/second |

## 📁 Project Structure
```
credit-card-pattern-matching/
│
├── pdc-project-sp22-bcs-010-and-032.cu  # Main CUDA source code
├── results.json                          # Performance metrics & statistics
├── sample_cards.json                     # Sample validated cards (1000 records)
└── README.md                            # This file
```

## 🔧 Installation & Compilation

### Prerequisites
- NVIDIA GPU with CUDA support
- CUDA Toolkit installed
- OpenMP compatible compiler

### Compilation Command
```bash
nvcc -arch=sm_75 -O2 -Xcompiler -fopenmp pdc-project-sp22-bcs-010-and-032.cu -o credit_card_validator
```

### Execution
```bash
./credit_card_validator
```

## 📈 Key Implementation Details

### 1. Card Generation (OpenMP)
- Parallel generation using OpenMP pragmas
- Random card number creation with proper prefixes
- Thread-safe random number generation

### 2. GPU Validation (CUDA)
- Kernel function: `validate_cards_kernel`
- 512 threads per block, dynamically calculated blocks
- Device functions for pattern matching and Luhn algorithm

### 3. Validation Logic
```c
// Pattern Matching
VISA: First digit = 4
MasterCard: First two digits between 51-55

// Luhn Algorithm
1. Double every second digit from right
2. If doubling > 9, sum the digits
3. Sum all digits
4. Valid if total % 10 == 0
```

## 📊 Output Files

### 1. `results.json`
Contains comprehensive performance metrics:
- Execution times (generation, validation, total)
- Card statistics (valid/invalid counts)
- Throughput calculations
- System configuration

### 2. `sample_cards.json`
First 1000 cards with validation results:
```json
[
  {
    "id": 1,
    "number": "4532167890123456",
    "type": "VISA",
    "valid": true
  }
]
```

## 🎯 Performance Optimizations
1. **GPU Parallelism**: Massively parallel validation using CUDA
2. **CPU Parallelism**: OpenMP for card generation and result aggregation
3. **Memory Optimization**: Efficient device memory management
4. **Kernel Optimization**: Minimized divergence, optimized arithmetic

## 📝 Sample Output
```
╔═══════════════════════════════════════════════╗
║       CREDIT CARD VALIDATION SUMMARY          ║
╚═══════════════════════════════════════════════╝

📊 Dataset Statistics:
   • Total Cards: 10,000,000
   • Valid Cards: ~1M (10.01%)
   • Invalid Cards: ~9M

⏱ Performance Metrics:
   • Generation Time: 5.9959 sec
   • Validation Time: 0.1722 sec
   • Total Execution: 6.1681 sec

Throughput:
   • Speed: 1.62 million cards/sec
```

## 🛠️ Hardware Used
- **GPU**: NVIDIA Tesla T4 (Google Colab Free Tier)
- **CPU**: 2-core with OpenMP support
- **Memory**: 12GB GPU memory

## 📚 Applications
- Financial systems testing
- Credit card processing simulations
- High-performance computing benchmarks
- Parallel algorithm demonstrations

## 👥 Authors
- BCS-010 & BCS-032
- Parallel and Distributed Computing Project

## 📄 License
Educational Use - Parallel Computing Project

## 🔍 Future Enhancements
1. Support for additional card types (American Express, Discover)
2. Real-time card validation API
3. Distributed computing across multiple GPUs
4. Machine learning integration for fraud detection

---

*Note: This project is for educational purposes only. Generated card numbers are random and not associated with real accounts.*
