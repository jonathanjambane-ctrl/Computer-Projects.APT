# ⚛️ Quantum Computing Projects

A collection of quantum computing projects built with IBM Qiskit, covering quantum teleportation protocols, circuit design, and qubit state visualization. Simulations run on IBM's cloud quantum servers.

---

## 📁 Projects

### 1. Quantum Teleportation Simulator
> Simulate the full quantum teleportation protocol using a 3-qubit circuit

Implements the quantum teleportation algorithm — one of the most fundamental protocols in quantum information science. Alice transfers an unknown qubit state |ψ⟩ to Bob using entanglement and 2 classical bits, without physically moving the qubit.

**What it demonstrates:**
- Bell pair creation via Hadamard + CNOT gates
- Quantum entanglement between Alice's and Bob's qubits
- Measurement-based state collapse and classical communication
- Bob's conditional Pauli-X / Pauli-Z corrections
- Teleportation fidelity = 1.0 on ideal simulator

**Tech Stack:** Python · IBM Qiskit · Jupyter Notebooks  
**Compute:** IBM Quantum Cloud (very low local laptop stress)  
**Core Skills:** Quantum logic gates · Qubit state manipulation · Bloch sphere visualization

---

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- A free [IBM Quantum account](https://quantum.ibm.com)
- Jupyter Notebook or JupyterLab

### Installation

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/quantum-projects.git
cd quantum-projects

# Install dependencies
pip install qiskit qiskit-ibm-provider jupyter
pip install qiskit[visualization] matplotlib pylatexenc
```

### IBM Cloud Authentication

```python
from qiskit_ibm_provider import IBMProvider

# First-time setup — paste your token from quantum.ibm.com
IBMProvider.save_account(token='YOUR_IBM_QUANTUM_API_TOKEN')
```

Get your free API token at 👉 [quantum.ibm.com](https://quantum.ibm.com) → Account → API Token

### Running the Teleportation Simulator

```bash
cd quantum_teleportation
jupyter notebook teleportation.ipynb
```

Or run directly:

```python
from qiskit import QuantumCircuit, QuantumRegister, ClassicalRegister, transpile
from qiskit_ibm_provider import IBMProvider

qr = QuantumRegister(3, 'q')
cr = ClassicalRegister(2, 'c')
qc = QuantumCircuit(qr, cr)

# Step 1: Create Bell pair
qc.h(1)
qc.cx(1, 2)

# Step 2: Alice encodes |ψ⟩
qc.cx(0, 1)
qc.h(0)

# Step 3: Alice measures
qc.measure([0, 1], [0, 1])

# Step 4: Bob corrects
qc.x(2).c_if(cr[1], 1)
qc.z(2).c_if(cr[0], 1)

# Run on simulator
provider = IBMProvider()
backend = provider.get_backend('ibmq_qasm_simulator')
job = transpile(qc, backend=backend)
print(qc.draw())
```

---

## 🔬 The Teleportation Protocol

```
q₀ (input) ──────────●──── H ──── M ─────────────────────────
                      │            ║
q₁ (Alice) ── H ──●──┼─────────── M ─────────────────────────
                  │  │            ║           ║
q₂  (Bob)  ──────⊕──────────────[X if c₁=1][Z if c₀=1]── |ψ⟩
```

| Step | Gate(s) | What Happens |
|------|---------|-------------|
| ① | H + CNOT | Bell pair created — q₁ and q₂ entangled |
| ② | CNOT + H | Alice encodes unknown state into entangled pair |
| ③ | Measure | Alice measures; 2 classical bits sent to Bob |
| ④ | X / Z | Bob applies corrections → recovers exact state |

---

## 📊 Supported Input States

| State | θ | φ | Bloch Vector |
|-------|---|---|-------------|
| \|0⟩ | 0° | 0° | (0, 0, +1) — north pole |
| \|1⟩ | 180° | 0° | (0, 0, −1) — south pole |
| \|+⟩ | 90° | 0° | (+1, 0, 0) |
| \|−⟩ | 90° | 180° | (−1, 0, 0) |
| \|R⟩ | 90° | 90° | (0, +1, 0) |

---

## 🔗 Resources

| Resource | Link |
|----------|------|
| Qiskit Documentation | [docs.quantum.ibm.com](https://docs.quantum.ibm.com) |
| IBM Quantum Platform | [quantum.ibm.com](https://quantum.ibm.com) |
| IBM Quantum Lab (Jupyter) | [quantum.ibm.com/lab](https://quantum.ibm.com/lab) |
| Qiskit GitHub | [github.com/Qiskit/qiskit](https://github.com/Qiskit/qiskit) |
| Qiskit Textbook (free) | [github.com/Qiskit/textbook](https://github.com/Qiskit/textbook) |
| Quirk Circuit Simulator | [algassert.com/quirk](https://algassert.com/quirk) |
| Qiskit YouTube | [youtube.com/@qiskit](https://www.youtube.com/@qiskit) |

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

> Built with [IBM Qiskit](https://qiskit.org) · Runs on [IBM Quantum Cloud](https://quantum.ibm.com)
