# NEXUS — References & What We Learned From Them

## 1. Domain-Driven Design — Martin Fowler

Reference: https://martinfowler.com/bliki/DomainDrivenDesign.html

### Relevant learning

DDD emphasizes building a domain model around the domain's language and rules, and using strategic boundaries such as Bounded Contexts for complex domains.

### NEXUS application

This supports explicitly separating the meanings of Inventory Document, Stock Movement, and Current Stock rather than treating all three as one generic inventory entity.

## 2. Bounded Context — Martin Fowler

Reference: https://martinfowler.com/bliki/BoundedContext.html

### Relevant learning

A Bounded Context defines where a particular model and vocabulary are valid.

### NEXUS application

The Inventory Foundation boundary is being defined explicitly so that inventory concepts retain precise meanings and do not absorb unrelated accounting or document concerns.

## 3. Domain Event — Martin Fowler

Reference: https://martinfowler.com/eaaDev/DomainEvent.html

### Relevant learning

A domain event captures something significant that happened in the domain and can provide a historical record useful for audit and debugging.

### NEXUS application

Stock Movement is conceptually aligned with an immutable record of an inventory effect. NEXUS is not being declared Event Sourced; the reference is used for the modeling distinction between an event/effect and current state.

## 4. Microsoft Dynamics 365 — Inventory On-hand

Reference: https://learn.microsoft.com/en-us/dynamics365/supply-chain/inventory/inventory-on-hand-list

### Relevant learning

Enterprise inventory systems distinguish on-hand inventory information from the underlying inventory/warehouse transactions and provide transaction-level investigation.

### NEXUS application

This supports keeping a current on-hand representation (`Current Stock`) distinct from historical inventory transactions (`Stock Movement`).

## 5. Oracle Inventory User's Guide

Reference: https://docs.oracle.com/cd/E26401_01/doc.122/e48820/T291651T292013.htm

### Relevant learning

Oracle's inventory documentation distinguishes on-hand quantity from inventory transaction information and treats inventory transactions as identifiable quantity-changing operations.

### NEXUS application

This reinforces the separation between the current quantity view/state and the transaction history.

## 6. Oracle Transaction Historical Summary

Reference: https://docs.oracle.com/cd/E18727_01/doc.121/e13450/T291651T295121.htm

### Relevant learning

Historical inventory quantities can be analyzed through inventory transactions and their sources.

### NEXUS application

This supports preserving immutable movement history instead of rewriting historical stock effects.

## Reference Policy

References are supporting material, not replacements for NEXUS business decisions.

A reference can inform terminology or architectural thinking, but an NEXUS Business Rule is accepted only when explicitly decided during domain discovery.
