# isHighPrioService - D365 Batch Job Sample

This repository contains the code for an X++ service in Dynamics 365 F&O, named `isHighPrioService`. The service's main function is to scan the sales and customer tables (`SalesTable` and `CustTable` respectively) and update the priority status of each Sales Order.


## Overview

The service class `isHighPrioService` includes a method named `process`. This method uses a transaction to safely update certain sales records. The criteria for these sales to be updated are:

1. The current priority of the sales record is set to No (indicated by `IsHighPrio::No`).
2. The corresponding customer's priority is set to Yes (`IsHighPrio::Yes`).

If both conditions are met, the priority of the sales record will be updated to Yes (`IsHighPrio::Yes`). The number of updated records will be logged and displayed to the user.

The controller class `isHighPrioController` is responsible for creating an instance of the `isHighPrioService` and running the `process` method.


## Assumptions

- The `IsHighPrio` field needs to exist in both `SalesTable` and `CustTable`. This field is assumed to be an enum with two values: `Yes` and `No`.
- The `AccountNum` field exists in `SalesTable` and is named `CustAccount`. This field is used to join the sales and customer tables together.


## Getting Started

The main entry point for this service is the `main` method in the `isHighPrioController` class. This method creates an instance of the controller, sets the execution mode and parameters, and starts the service operation.


## Error Handling

If an error occurs during the operation, the transaction will be aborted (`ttsabort`), and an error message will be logged and displayed to the user.

## Contract Class

Currently, the `isHighPrioContract` class is an empty class decorated with `DataContractAttribute`. It serves as a placeholder for any future implementation where you may need to pass specific parameters to the `process` method. If any future parameters are required for the `process` method, they would be added as properties to this class.

## Note

Please refer to the Dynamics AX documentation for more information about SysOperation framework, which is used here to implement batch service operations.