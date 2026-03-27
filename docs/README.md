# COBOL Legacy Code Documentation

## Overview
This directory contains documentation for the COBOL legacy codebase related to student account management.

## COBOL Files

### File Structure
| File Name | Purpose | Key Functions | Business Rules |
|-----------|---------|----------------|-----------------|
| {filename_1} | {description} | {functions} | {rules} |
| {filename_2} | {description} | {functions} | {rules} |

## Student Account Business Rules
- {rule_1}
- {rule_2}
- {rule_3}

## Getting Started
Refer to individual COBOL file documentation for detailed implementation specifics.

## Data Flow Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant Main as MainProgram
    participant Ops as Operations
    participant Data as DataProgram

    User->>Main: Interact with Menu
    Main->>Main: Display Menu Options
    User->>Main: Enter Choice (1-4)
    
    alt Choice = 1: View Balance
        Main->>Ops: CALL 'Operations' USING 'TOTAL'
        Ops->>Data: CALL 'DataProgram' USING 'READ'
        Data->>Data: Retrieve STORAGE-BALANCE
        Data-->>Ops: Return Current Balance
        Ops->>User: Display "Current balance: {amount}"
    else Choice = 2: Credit Account
        Main->>Ops: CALL 'Operations' USING 'CREDIT'
        User->>Ops: Enter Credit Amount
        Ops->>Data: CALL 'DataProgram' USING 'READ'
        Data-->>Ops: Return Current Balance
        Ops->>Ops: ADD Amount to Balance
        Ops->>Data: CALL 'DataProgram' USING 'WRITE'
        Data->>Data: Update STORAGE-BALANCE
        Ops->>User: Display "Amount credited. New balance: {amount}"
    else Choice = 3: Debit Account
        Main->>Ops: CALL 'Operations' USING 'DEBIT'
        User->>Ops: Enter Debit Amount
        Ops->>Data: CALL 'DataProgram' USING 'READ'
        Data-->>Ops: Return Current Balance
        alt Sufficient Funds
            Ops->>Ops: SUBTRACT Amount from Balance
            Ops->>Data: CALL 'DataProgram' USING 'WRITE'
            Data->>Data: Update STORAGE-BALANCE
            Ops->>User: Display "Amount debited. New balance: {amount}"
        else Insufficient Funds
            Ops->>User: Display "Insufficient funds for this debit."
        end
    else Choice = 4: Exit
        Main->>User: Display "Exiting the program. Goodbye!"
        Main->>Main: STOP RUN
    end
    
    Main->>Main: Return to Menu (unless Exit selected)
```
