# Logical Operations in a Polygon zkSNARK Circuit Implementation

## Introduction:
Welcome to this GitHub repository dedicated to the implementation of a Polygon zkSNARK Circuit that focuses on logical operations. The purpose of this project is to develop and deploy a Zero-Knowledge Succinct Non-Interactive Argument of Knowledge (zkSNARK) circuit on the Polygon blockchain network. This custom circuit incorporates a logical gate to facilitate secure and privacy-preserving computations.

The primary objective of this repository is to construct the circuit using the circom programming language, known for its efficiency and flexibility in designing zkSNARK circuits. The integrated logical gate enables users to perform confidential operations while keeping sensitive inputs hidden from the public eye.

## Getting Started

### Setup

To engage with this project, follow these steps:

1. Download the Circom programming language from the official website: [Circom](https://www.circom.io/).
2. Install Circom on your system by following the instructions in the documentation.

### Running the Program

To execute the circuit, follow these instructions:

1. Open your terminal or command prompt and navigate to the designated project directory.
2. Compile the circuit by executing the following command:

```bash
npm install
```

3. After a successful installation, proceed to compile the circuit:

```bash
npx hardhat circom
```

4. Deployment: The circuit is deployed on the Polygon Mumbai testnet, but you can choose a different suitable testnet:

```bash
npx hardhat run scripts/deploy.ts --network mumbai
```

## Circuit Logic

The circuit logic is established using Circom and consists of three templates for fundamental logic gates: AND, OR, and NOT. The core customized circuit named 'LooseCircuit' is built using these gate templates.

### AND Gate

The AND gate template takes two input signals, 'a' and 'b,' producing an output signal 'out' that represents the logical AND operation between 'a' and 'b.'

```circom
template AND() {
    signal input a;
    signal input b;
    signal output out;

    out <== a * b;
}
```

### OR Gate

The OR gate template accepts two input signals, 'a' and 'b,' and generates an output signal 'out' representing the logical OR operation between 'a' and 'b.'

```circom
template OR() {
    signal input a;
    signal input b;
    signal output out;

    out <== a + b - a * b;
}
```

### NOT Gate

The NOT gate template takes an input signal 'in' and produces an output signal 'out' signifying the logical NOT operation applied to 'in.'

```circom
template NOT() {
    signal input in;
    signal output out;

    out <== 1 + in - 2 * in;
}
```

### Custom Circuit - Multiplier2

The primary customized circuit, 'Multiplier2,' leverages the AND, NOT, and OR gates to implement the logic for multiplying input values 'a' and 'b,' resulting in the output 'q.'

```circom
pragma circom 2.0.0;

/* This circuit template verifies that 'c' results from the multiplication of 'a' and 'b'. */

template Multiplier2 () {

    // Input signals 'a' and 'b'
    signal input a;
    signal input b;

    // Signals from the gates
    signal x;
    signal y;

    // Final output signal 'q'
    signal output q;

    // Components used in the circuit
    component andGate = AND();
    component orGate = OR();
    component notGate = NOT();

    // Circuit logic

    andGate.a <== a;
    andGate.b <== b;
    x <== andGate.out;

    notGate.in <== b;
    y <== notGate.out;

    orGate.a <== x;
    orGate.b <== y;
    q <== orGate.out;
}

// Below are the templates of the gates used in the circuit logic

template AND() {
    signal input a;
    signal input b;
    signal output out;

    out <== a * b;
}

template OR() {
    signal input a;
    signal input b;
    signal output out;

    out <== a + b - a * b;
}

template NOT() {
    signal input in;
    signal output out;

    out <== 1 + in - 2 * in;
}

component main = Multiplier2();
```

Following the installation and execution steps will result in the successful implementation of the circuit, providing the desired output 'q' based on the given 'a' and 'b' inputs.

## Support
If you encounter challenges or have questions about the program, refer to the official Circom documentation or seek assistance from the community.

# Author
[Simran](21bcs3832@cuchd.in)

License
This project is licensed under the MIT License.
