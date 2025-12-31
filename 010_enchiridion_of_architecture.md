# Architectural Boundaries

> Thinking about architecture makes only sense if a feature has shared logic, multiple entry points, or real domain rules else don't. Trivial CRUD pages (single screen, little logic). Direct UI → route → DB is faster and clearer.


Architecture defines a set of components of a system. How these components are arranged within a system. How these components communicate with each other. What kind of boundaries | exist between the components. We use boundaries | to separate components from each other that shouldn't know about each other. This gives us isolation within the system that makes the system robust on itself if component failure within the system happens. One component cannot crash the whole system. Proper boundaries will give the possibility to make the components maintainable, extendable, which is in essense a base on which to build up.

Boundaries group things together that change together at the same time and the same rate(?). At the same rate means they change together if requirements change. This is single reponsobility principle (SRP). A module has one reason to change. A module is not a component a module is a BOUNDARY. The whole folder is one module: 
- responsibility: billing
- reasons to change: pricing/payment rules
- public API: exported functions form index.ts

```
lib/
 └── billing/
     ├── stripe.ts
     ├── plans.ts
        └── index.ts

```
There are horizontal and vertical slicing of boundaries. Horizontal boundaries are layer for the api, for the logic for the database. Vertical slicing creates boundaries between different features of the system. Feature of customer management can be separate from feature of bookings management. Vertical slice is organized by feature and not by technical layer. Each vertical slice own its UI, core, persistance. But usually each slice owns its behavior but shares infrastructure. Microservices is a vertical slicing where each service/team retains their own everything down to the database.

```
features/
  createOrder/
    handler.ts
    usecase.ts
    repo.ts

shared/
  db/
    connection.ts
  ui/
    Button.tsx
```

Boundaries can be separated by source-level: classes, methods, functions. The communication between boundaries happens with simple method calls. **For monolith systems these are the only boundaries in the system.** Not visible at deploy-time.
Dynamically-linked deployable components. Separated components can be developed and deployed on their own. But run in the same address space and communicate via simple methods calls. As boundary there are local processes that can communicate via a socket. Services (micro-services) form the strongest level of a boundary. Services live on different machines and communicate over a network. Services have own databases. **You can combine different kind of boundaries as needed.**

Boundaries have costs. Deveopment effort + maintainability. They have trade-offs and this you must assess as a developer.

> If you have five teams working on a system, they will likely benefit from having five clearly separated parts with stable interfaces connecting them. The same architecture could be harmful to productivity if there is only a single small team working on the system.

If you need to decide and you don't know, keep it simple! If it is not clear if boundary is needed a good sign for over-engineering. If you don't understand the abstractions (boundaries) of the sysem, you did it wrong (you are not alone!). This is bad architecture.

Adding more boundaries is expensive. System evolve, boundaries evolve, architecture evolve. If system or team grows, additional boundaries are needed to maintain productivity.

Boundaries help to delay decisions. Build a system without connecting to the real database using in-memory and later swap against real database. Boundaries enable clean separation between UI, LOGIC, STORAGE. This helps to swap out of any of the components without affecting the whole system. Change UI keep the logic and the storage or change the logic, keep the UI and the storage. It is important for our system to allow change. Boundaries allow change in the system!

```
  Micro‑hex in simple words

  - Build each feature as a tiny, self‑contained module.
  - Put business rules in the center (“core”), and keep it independent of React, fetch, DB, or
    frameworks.
  - The core talks to the outside world through interfaces (ports).
  - The real world (HTTP, DB, UI) implements those interfaces (adapters).
  - This keeps logic reusable and stops it from being duplicated in every screen.

  Think: “Core rules in the middle, adapters at the edges.”

  Implementation in this repo (availability)

  - src/features/availability/domain/
    Pure rules: date normalization, day‑key generation, “is date unavailable?” logic.
  - src/features/availability/application/
    Ports + use‑cases (load availability, save range, update, delete).
  - src/features/availability/adapters/http/
    Real API calls to /api/petsitter/unavailability and /api/petsitter/services.
  - src/features/availability/ui/
    Hook (useAvailabilityCalendar) and shared view (AvailabilityCalendarView) for React.
  - src/features/availability/index.ts
    The only public API others import.

  Simple data flow

  UI (hook) -> Use‑case (core) -> Port interface -> Adapter (HTTP/DB)

  Alternate names

  - Ports & Adapters
  - Hexagonal Architecture
  - Clean Architecture (feature‑slice version)
  - Onion Architecture (conceptually similar)
  - Vertical Slice Architecture (when combined with feature folders)

• Read flow (load availability + services)

  AvailabilityCalendarView (src/features/availability/ui/components/
  AvailabilityCalendarView.tsx)
    -> useAvailabilityCalendar hook (src/features/availability/ui/hooks/
  useAvailabilityCalendar.ts)
      -> loadAvailability use-case (src/features/availability/application/use-cases.ts)
        -> UnavailabilityRepository.list port (src/features/availability/application/ports.ts)
          -> HTTP adapter (src/features/availability/adapters/http/unavailability-repo.ts)
            -> API route (src/app/api/petsitter/unavailability/route.ts)
        -> ServicesRepository.listEnabled port (src/features/availability/application/ports.ts)
          -> HTTP adapter (src/features/availability/adapters/http/services-repo.ts)
            -> API endpoint `/api/petsitter/services`
      -> derive unavailable day keys (src/features/availability/domain/availability.ts)

  Save flow (create new unavailability range)

  User selects range in AvailabilityCalendarView (src/features/availability/ui/components/
  AvailabilityCalendarView.tsx)
    -> actions.saveRange in hook (src/features/availability/ui/hooks/
  useAvailabilityCalendar.ts)
      -> saveRange use-case (src/features/availability/application/use-cases.ts)
        -> UnavailabilityRepository.create port (src/features/availability/application/
  ports.ts)
          -> HTTP adapter (src/features/availability/adapters/http/unavailability-repo.ts)
            -> API route (src/app/api/petsitter/unavailability/route.ts)
      -> refresh list + recompute day keys (src/features/availability/domain/availability.ts)

• Use micro‑hex only when it earns its cost. Don’t use it for:

  - Trivial CRUD pages (single screen, little logic). Direct UI → route → DB is faster and
    clearer.
  - One‑off UI experiments that might be thrown away. Keep it lightweight.
  - Tightly coupled legacy areas where adding boundaries would fight the existing structure.
  - Pure UI components (no business rules). A slice adds ceremony without value.
  - Time‑critical hotfixes. Patch first, refactor later.

  Rule of thumb: if the feature has shared logic, multiple entry points, or real domain rules,
  use micro‑hex. If it’s just “fetch and render a table,” don’t.



```
Resources:
- https://convincedcoder.com/2019/04/27/Software-architecture-boundaries/
