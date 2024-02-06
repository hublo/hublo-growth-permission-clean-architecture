---
title: Leveraging Clean Architecture For Enhanced Permission Management
# separator: <!--s-->
# verticalSeparator: <!--v-->
theme: moon
# revealOptions:
#   transition: 'fade'
---
### SOLID Principles
![SOLID](./images/solid.png)
---
**Single Responsibility Principle (SRP):** A class should have only one reason to change.
----
#### DON'T DO THIS
It may look suitable for a developer to have only one method to get shifts from an hubler
```typescript
class Hubler {
  getShifts() {
    // send shifts done by hubler
  }
}
```
Note: Je parle ici e mes grosses baloches
----
#### DO THIS
Getting shifts of a given hubler is not the same if we want to display the calendar or if we want to know their planning from an admin point of view as different rules may apply to retrieve them
```typescript
class HublerPlanning {
  getShifts() {
    // send shifts done by hubler
  }
}

class InstitutionHublerAvailabilities {
  getShifts() {
    // send shifts done by hubler in an institution
  }
}
```
---
**Open/Closed Principle (OCP):** Software entities should be open for extension, but closed for modification.
----
#### DON'T DO THIS
<span style="font-size: 0.8em">

```typescript
class Shift {
  post() {
    // save in DB
    this.notify();
  }
  notify() {
    // send notification to hubler of the institution
  }
}
class HubloPoolShift extends Shift {
  notify() {
    // send notification to hublo poolers
  }
}
```

</span>

----
#### DO THIS
```typescript
abstract class Shift {
  post() {
    // save in DB
    this.notify();
  }
  abstract notify();
}

class HubloPoolShift extends Shift {
  notify() {
    // send notification to hublo pool
  }
}

class NativeShift extends Shift {
  notify() {
    // send notification to hubler
  }
}
```
---
**Liskov Substitution Principle (LSP):** Subtypes must be substitutable for their base types.
----
#### DON'T DO THIS
```typescript
class Notification {
  send() {
    console.log('Notification sent')
  }
}

class ScheduledNotification extends Notification {
  send() {
    throw new Error('Sending directly a scheduled notification is not allowed')
  }
}
```
----
#### DO THIS
```typescript
abstract class Notification {
  abstract send();
}

class ScheduledNotification extends Notification {
  send() {
    console.log('Notification scheduled')
  }
}

class InstantNotification extends Notification {
  send() {
    console.log('Notification sent')
  }
}

```
---
**Interface Segregation Principle (ISP):** No client should be forced to depend on methods it does not use.
----
#### DON'T DO THIS
```typescript
interface UserShiftService {
  createShift();
  getShift();
  fillShift();
  updateShift();
}
```
----
#### DO THIS
```typescript
interface HublerShiftService {
  getShift();
  fillShift();
}

interface AdminShiftService {
  createShift();
  updateShift();
}
```
---
**Dependency Inversion Principle (DIP):** Depend on abstractions, not on concretions.
----
#### DON'T DO THIS
For each persistence we need to redefine a whole new service even if the business logic is the same
```typescript
class ShiftOfferService {
  constructor() {
    this.db = new ShiftOfferMongoDB();
  }
  
  postShiftOffer() {
    this.db.save();
  }
}

class HubloPoolShiftOfferService extends ShiftOfferService {
  constructor() {
    this.db = new HubloPoolShiftOfferMongoDB();
  }
}

class TestShiftOfferService {
  constructor() {
    this.db = new InMemoryDb();
  }
}
```
----
#### DO THIS
You inject the accurate persistence layer directly
```typescript
interface ShiftOfferRepository {
  save();
}

class MongoDBShiftOfferRepository implements ShiftOfferRepository {
  //...
}

class ShiftOfferService {
  constructor(private db: ShiftOfferRepository) {}
  
  postShiftOffer() {
    this.db.save();
  }
}
```
---
