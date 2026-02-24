# Task: Implement Purchase Flow for Coca-Cola in Store

## Description
Develop a user interface flow for purchasing Coca-Cola in a store. The flow should include interaction with a cashier, selection between Light and Regular Coca-Cola, and choice of payment method (cash or card).

## Expected Results
- The user can interact with a virtual cashier.
- The user can choose between Coca-Cola Light and Regular.
- The user can select a payment method (cash or card).
- The process completes with confirmation of purchase.

## Acceptance Criteria
- The flow matches the diagram below.
- All choices (type of Coca-Cola and payment method) are available and functional.
- The user receives a confirmation at the end of the process.

## Flow Diagram

```mermaid
graph TD
    A[Customer enters the store] --> B[Approaches the cashier]
    B --> C[Cashier: "Which Coca-Cola do you want? Light or Regular?"]
    C --> D[Customer chooses Light]
    C --> E[Customer chooses Regular]
    D --> F[Cashier: "How would you like to pay? Cash or Card?"]
    E --> F
    F --> G[Customer pays with Cash]
    F --> H[Customer pays with Card]
    G --> I[Cashier gives Coca-Cola Light/Regular]
    H --> I
    I --> J[Purchase complete]
