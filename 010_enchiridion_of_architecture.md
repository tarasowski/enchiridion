# Architectural Boundaries

Architecture defines a set of components of a system. How these components are arranged within a system. How these components communicate with each other. What kind of boundaries | exist between the components. We use boundaries | to separate components from each other that shouldn't know about each other. This gives us isolation within the system that makes the system robust on itself if component failure within the system happens. One component cannot crash the whole system. Proper boundaries will give the possibility to make the components maintainable, extendable, which is in essense a base on which to build up.

Boundaries can be vertical UI <|> LOGIC >|> STORAGE and can be horizonal component 1 <|> component 2 <|> component 3. If the components don't know anything about each other like the logic doesn't know about the database we use, we can simply change out the database, or if ui doesn't know anything about the business logic (dumb UI), we can change the business logic easily.

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
