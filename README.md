# Loan Management System

This loan management system is a decentralized application (dApp) built on the Internet Computer platform. It allows borrowers to request loans backed by collateral and lenders to provide funds for these loans. The system ensures transparency, security, and fairness in loan transactions.

## Table of Contents

- [Loan Management System](#loan-management-system)
    - [Table of Contents](#table-of-contents)
    - [Overview](#overview)
    - [Features](#features)
    - [Project Structure](#project-structure)
    - [Key Functions](#key-functions)
    - [Getting Started](#getting-started)
        - [Prerequisites](#prerequisites)
        - [Installation](#installation)
    - [Usage](#usage)
    - [License](#license)

## Overview

The Loan Management System aims to facilitate peer-to-peer lending by connecting borrowers and lenders in a decentralized manner. It leverages smart contracts on the Internet Computer to enable secure and transparent loan transactions without the need for intermediaries.

## Features

- Borrowers can request loans by providing collateral.
- Lenders can fund loans and earn interest on their investments.
- Smart contracts ensure trustless and transparent loan agreements.
- Borrower and lender profiles for tracking transaction history.
- Integration with the Internet Computer Ledger for secure payments and settlements.

## Project Structure

The project follows a structured organization to maintain modularity and clarity:

- **`canisters/`**: Contains the smart contract canisters written in Motoko.
- **`src/`**: Frontend source code for the user interface.
- **`scripts/`**: Scripts for deployment, testing, and other utilities.
- **`tests/`**: Test suites for ensuring code correctness and reliability.
- **`docs/`**: Documentation files, including README, API reference, and contributing guidelines.

## Key Functions

The Loan Management System provides several essential functions to manage loan transactions:

- **`addLoan(payload: LoanPayload): Result<Loan, ErrorType>`**: Allows borrowers to add a new loan request, specifying details such as title, description, collateral, and loan amount.
- **`getLoans(): Vec<Loan>`**: Retrieves a list of all active loans available in the system.
- **`addRequest(loanId: text, description: text, amount: nat64): Result<Request, ErrorType>`**: Enables borrowers to submit a loan request for a specific loan ID, including the desired loan amount and description.
- **`getRequests(): Vec<Request>`**: Fetches all loan requests submitted by borrowers.
- **`selectRequest(requestId: text): Result<Loan, ErrorType>`**: Allows lenders to select a loan request by ID, providing funds and marking the loan as assigned.
- **`createPaymentPay(loanId: text): Result<ReservePayment, ErrorType>`**: Initiates the payment process for a loan, creating a payment reservation for the borrower to fulfill.
- **`completePayment(reservor: Principal, loanId: text, reservePrice: nat64, block: nat64, memo: nat64): Result<ReservePayment, ErrorType>`**: Verifies and completes the payment reservation initiated by the borrower, updating the payment status accordingly.
- **`createRePayment(loanId: text, amount: nat64): Result<ReserveRePayment, ErrorType>`**: Facilitates the repayment process for borrowers, creating a repayment reservation for the specified loan and amount.
- **`completeRePayment(reservor: Principal, loanId: text, reservePrice: nat64, block: nat64, memo: nat64): Result<ReserveRePayment, ErrorType>`**: Verifies and completes the repayment reservation initiated by the borrower, updating the repayment status accordingly.

## Getting Started

### Prerequisites

To run the Loan Management System locally, you need:

- [Node.js](https://nodejs.org/) installed on your machine.
- An Internet Computer development environment set up (e.g., using DFX).

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/loan-management-system.git
   ```

2. Install dependencies:

   ```bash
   cd loan-management-system
   npm install
   ```

## Usage

To deploy all canisters, follow these steps:

```bash
# Start DFX
dfx start --background --clean

# Deploy Ledger Canister
./deploy-local-ledger.sh

# Deploy Internet Identity
dfx deploy internet_identity

# Generate types declarations
dfx generate dfinity_js_backend

# Deploy Backend Canister
dfx deploy dfinity_js_backend

# Deploy Frontend Canister
dfx deploy dfinity_js_frontend

# Transfer Tokens to Principal used on the frontend
dfx identity use default
dfx ledger transfer <ADDRESS>  --memo 0 --icp 100
```

Replace <ADDRESS> with the address of the recipient. To get the address from the principal, you can use the helper function from the marketplace canister - getAddressFromPrincipal(principal: Principal).

## License

This project is licensed under the [MIT License](./LICENSE).
