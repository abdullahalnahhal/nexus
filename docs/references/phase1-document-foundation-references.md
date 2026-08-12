# NEXUS — Phase 1 Document Foundation References

## Reference Classification

This document records external concepts that informed the Foundation. External references do not prescribe NEXUS behavior; NEXUS business discovery defines the final rules.

## 1. Domain-Driven Design — Eric Evans

**What we learned:** business concepts and behavior should drive the domain model, and shared language should be explicit.

**NEXUS use:** the Document Foundation distinguishes shared concepts from Document-specific lifecycles instead of forcing one generic model on every document.

## 2. Domain Modeling — Martin Fowler

**What we learned:** domain models should represent business behavior and meaningful relationships.

**NEXUS use:** Document References model relationship semantics explicitly through a relationship type rather than relying on raw foreign keys alone.

## 3. Requirements Engineering — Ian Sommerville

**What we learned:** system behavior should be expressed as traceable requirements and constraints.

**NEXUS use:** Document Foundation decisions are written as explicit rules and kept separate from implementation-specific concerns.

## 4. Audit / Activity Logging Concepts

**What we learned:** auditability and user activity are distinct concerns from business history.

**NEXUS use:** Spatie Activity Log handles user activity, while Domain-specific business history remains separate when required.

## 5. Spatie Laravel Permission

**What we learned:** authorization can be expressed as named permissions grouped by roles.

**NEXUS use:** permission names represent operations, while scope is represented separately across Company/Branch/Warehouse/POS contexts. This preserves the NEXUS rule that authorization is permission-based rather than hardcoded by job title.

## 6. Spatie Media Library

**What we learned:** attachments can be managed through media collections and reusable metadata/storage infrastructure without creating a custom generic attachment storage model.

**NEXUS use:** Documents use Spatie Media Library for image/PDF attachments; attachment requirements remain business/document-specific.

## NEXUS Decision Boundary

References informed the vocabulary and design principles only. The actual NEXUS Document Foundation decisions were established through NEXUS Business Discovery.
