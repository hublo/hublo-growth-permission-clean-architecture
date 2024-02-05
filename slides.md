---
title: Leveraging Clean Architecture For Enhanced Permission Management
# separator: <!--s-->
# verticalSeparator: <!--v-->
theme: moon
verticalSeparator: "---vertical"
# revealOptions:
#   transition: 'fade'
---
# Plan

- Introduction
- Context
- Etc.

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

## Why clean architecture?

- Define clean architecture and its relevance to the project (SOLID, etc.)
![SOLID](./images/solid.png)

- Explain the alignment of **clean** architecture principles with the project's goals.

---

## Architecture Overview 

![Clean architecture](./images/clean-archi-1.png)

---

## Architecture Overview 

![Clean architecture](./images/clean-archi-2.png)

---

### Implementation
#### Code Organization: Base organization


![Implementation](./images/code_org/base.drawio.png)
<img src="./images/clean-archi-1.png" alt="image" width="40%" height="auto" style="margin:0 0 0 4em">


---

### Implementation
#### Code Organization: Business logic

![Implementation](./images/code_org/business_logic.drawio.png)

---vertical

### Implementation
#### Business logic: Entity example 

```typescript
// permission.entity.ts
export abstract class Permission extends SoftDeleteEntity {
  // [...]

  protected _category: PermissionCategory
  get category() {
    return this._category
  }

  organize(category: PermissionCategory) {
    if (category.isMainCategory()) {
      throw new InvalidPermissionCategoryHierarchyError()
    }
    this._category = category
  }
}
```

---vertical

### Implementation
#### Business logic: Port example 
> **Use Case <- PORT (interface) -> Repository**

```typescript
// permission.port.ts
export interface PermissionPort {
  /**
   * @throws { PermissionNotFoundError }
   */
  findById(id: string): Promise<Permission>
}
```

---vertical

### Implementation
#### Business logic: Use case example 

<span style="font-size:0.7em;">

```typescript
// get-all-permissions.use-case.ts
@Injectable()
export class GetAllPermissions {
  constructor(@Inject(PermissionPort) private permissionPort: PermissionPort) {}

  public async execute(): Promise<PermissionListItemOutput[]> {
    const permissions = await this.findAllPermissions()
    return this.mapOutput(permissions)
  }

  private findAllPermissions(): Promise<Permission[]> {
    return this.permissionPort.findAll()
  }

  private mapOutput(permissions: Permission[]) {
    return permissions.map((permission) =>
      PermissionMapper.toListItemOutput(permission),
    )
  }
}
```
</span>

---


### Implementation
#### Code Organization: Infrastructure

![Implementation](./images/code_org/infrastructure.drawio.png)

---


### Implementation
#### Code Organization: Tests

![Implementation](./images/code_org/tests.drawio.png)

---
