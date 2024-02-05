# How we did Clean Architecture

## Introduction (1 min)

- Briefly introduce the team and the topic. (1 slide)
- 1 sentence to introduce the plan. (1 slide)

## Context (2 min)

- New project Prmission. White card (1 slide)
- Dealing with heavy legacy sails JS (1 slide)
- How to do it profitable to HUBLO and tech team. Think Platform. (1 slide)

## Clean Architecture (10 min) "TOM/PIERRE"
 
- to be planned and designed

## How we did it (15 min) "AMROU/VALENTIN"

- to be planned and designed

- Clean archtecture
- From Controller Side, we used nestjs (built-ins), external trigger
  - (nest-built-in) decorators pattern for
    - parsers (For incomming)
    - validations/transformations (For incomming)
    - documentation (openapi)
    - ...
    - and also, 
    - Guards (authn & authz), 
    - ~~Filter~~
    - Interceptors + AOP (Aspect oriented programming) , as error handlers 
  - letting us having a DRY and declarative code
  - So that we managed to prepare the Data Transfer Object (DTO) to be passed as expected to use case
  - ??To know, that even if guards are business related, since those are project wide usage, we declare them on the controller but those are project-wide used??

  

## Benefits of the Chosen Approach (5 min) "TOM/VALE"

- Clean Code and Maintainability: 
  - readability, clear function name
  - Discuss how clean architecture and TypeScript contribute to cleaner
  - more maintainable code.
  - etc.
- Some DDD principles : 
  - Entity encapsulate business logic
- Enhanced Testing: Explain how the approach leads to more realistic and manageable unit tests (stubs, etc.)
- Developer Experience: Share insights on how this approach makes coding more enjoyable and efficient.

## Challenges and Downsides (5 min)

- Code Volume: Address the concern of increased code lines due to clean architecture and TypeScript.
- Compatibility Issues: Discuss compatibility challenges (Prisma, mixins, etc.).
- Learning Curve: Acknowledge the learning curve associated with clean architecture and TypeScript for new team members.
- Discuss the role of TypeScript and NestJS in this architecture (Mixin, etc.)

## Conclusion (2 min)

- Summarize the key points.
- Highlight the outcomes and lessons learned.
- Reiterate the value of using TypeScript, NestJS and clean architecture in your specific context.

## Q&A Session (5 min)

- Open the floor for questions.
- Prepare to address anticipated questions based on the presentation content.
