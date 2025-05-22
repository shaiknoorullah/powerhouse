### Summary
The Rule Engine package is a typescript package that allows developers to dynamically build conditions.
This is possible with the following features exposed via the package.
1. Access to Atomic conditions and their functions based on the selected Operand type, Operator Type and Rule Type
2. Ability to parse and evaluate the conditions on dynamic input at runtime
3. Add operators, operands, rule types and functions through the exposed API.
### Motivation
It is no surprise that conditions are the most used part of any programming language, at the heart of any logic - we find conditions. But what if, I want to give the control over my logic to the end user through a visual builder or reuse/share a condition between multiple services / code blocks. This presents a unique and interesting problem for us:

> [!INFO] Charecteristics
> - Deterministic
> - Idiomatic
> - Idempotent
> - Composable (Atomicity)
> - Reusable
> - Maintainable (debuggability and reproducibility)


### Proposed Solution
According to the aforementioned requirements or characteristics, A high level plan is proposed in the following section.

#### Architecture
![[Rule Engine Package 2025-04-24 17.19.40.excalidraw]]

![[Rule Engine Package 2025-04-24 17.34.04.excalidraw]]


#### Specification
The proposed solution is built upon some ideas.
1. Any condition is nothing but a `factual statement` that can be evaluated to either `true` or `false`
2. These statements can be combined together to compose complex statements

##### Data Hierarchy
Every Rule or Condition can be divided into a few types:

**Evaluation**:
Evaluation is the most simplest form of a conditional statement. In essence at its core, it is nothing but a mathematical equation (sort of..) examples include: 
```typescript
if(string.length>0)
```

**Validation**:
Validations are a superset type of Evaluation rules. These can be complex and are used to validate any one thing to other. for example: validating a request object or a response json. there might be several sub types in validations as well ranging between syncronous and asyncronous validations for data type validations or signature validations.

**Authorization**:
Authorization is a special type of evaluation. As its name suggests, it is for the sole purpose of authorization it can authorize users/services/external requests/etc and provide a result as `can` or `cannot` based on the `ABAC` + `IBAC`+`PBAC` authorization system.

#### Implementation Details
The implementation will have three parts.
1. functions repository:
   A functions repository will be a folder (preferably on minio) where functions will be stored where each file will represent one function. 
   following the below described rules:
	1. It is independent of external libraries/packages
	2. It is pure and atomic (it only has one single function)
	3. named export, instrumentable, wrappable in callbacks, and verbosable
	4. these functions can not be mutable by the developers of this package but only generated (packaged, minified, optimized, wrapped) through the api.
2. Class based system which will implement the logic for all the above mentioned features. Must follow all OOPs patterns. especially the `factory` pattern and `singleton` patterns. composability and ease of use for the frontend devs (using react-flow) and the backend devs with type intellisense is key here.api

[[technical_spec|Technical Specification]]

