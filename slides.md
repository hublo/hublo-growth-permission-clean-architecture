---
title: Leveraging Clean Architecture For Enhanced Permission Management
# separator: <!--s-->
# verticalSeparator: <!--v-->
theme: moon
# revealOptions:
#   transition: 'fade'

---

## Introduction
- Team
- Topic
- Objectives of the presentation.
  - objective 1
  - objective 2
  - objective 3

> Best Team Ever.

Note: speaker notes FTW!
---

## Context
- Brand New Project. FREEEDOM! gif Frozen
- We are stuck with a legacy system (serviceApp => Sails.js). gif Titanic
- We need to manage permissions. gif Matrix

---

## Clean Architecture

---

### What is Clean Architecture?
- **Purpose:** Design software with loose coupling and high cohesion.
- **Structure:** Organized into layers with:
  - **Entities** at the core (business objects and rules).
  - **Use Cases** encapsulating business logic.
  - **Interface Adapters** translating between web, database, and external agency formats.
  - **Frameworks & Drivers** as the outermost layer (UIs, databases).
- **Key Concept:** Dependency Rule - Dependencies must point inward, from outer layers to inner layers.

---

### SOLID Principles
solid-principles.md

---

---

### Benefits of Clean Architecture
- **Flexibility:** Easily adapt to new requirements without significant rework.
- **Testability:** Independent layers allow for unit testing of business logic without UI, database, or external dependencies.
- **Maintainability:** Simplified updates and enhancements with minimal impact on existing functionality.
- **Readability:** Clear separation of concerns makes it easier for product managers and new developers to understand the system structure.
- **Framework Independence:** Business rules are not tied to the technology stack, making it easier to switch frameworks or libraries.

---

## Architecture Overview 

![Clean architecture](./images/clean-archi-1.png)

---

## Architecture Overview 

![Clean architecture](./images/clean-archi-2.png)
