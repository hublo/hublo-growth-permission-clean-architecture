---
title: Leveraging Clean Architecture For Enhanced Permission Management
theme: ./theme/hublo.css
# revealOptions:
#   transition: 'fade'
---

# Clean architecture

---

## Details

----

### The database

_<small>Don't base your data model on how it's actually stored</small>_

----

### The framework

_<small>Don't comply to the framework. Use the framework to comply to your business</small>_

----

### The interface

_<small>Don't tie your business to your interface</small>_

---

## Not details

----

### The business rules

----

#### **The entities**

- Object that contain of have easy access to business data
- They implement the critical business rules that operate on that data
- They are not plain-old TS objects representing the DB schema

----

#### **The use cases**

- They define the way an automated system is used
- They specify the inputs to be provided and outputs to be returned to the user
- They describe application-specific business rules
- They don't know in which environment they are running

---

## The dependency rule

<img src="./images/clean-archi-1.png" height="500">

---

## A use-case, step by step


