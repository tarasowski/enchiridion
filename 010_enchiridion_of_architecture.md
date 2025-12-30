# Architectural Boundaries

Architecture defines a set of components of a system. How these components are arranged within a system. How these components communicate with each other. What kind of boundaries | exist between the components. We use boundaries | to separate components from each other that shouldn't know about each other. This gives us isolation within the system that makes the system robust on itself if component failure within the system happens. One component cannot crash the whole system. Proper boundaries will give the possibility to make the components maintainable, extendable, which is in essense a base on which to build up.

Boundaries can be vertical UI <|> LOGIC >|> STORAGE and can be horizonal component 1 <|> component 2 <|> component 3. If the components don't know anything about each other like the logic doesn't know about the database we use, we can simply change out the database, or if ui doesn't know anything about the business logic (dumb UI), we can change the business logic easily.

Boundaries group things together that change together at the same time and the same rate(?). At the same rate means they change together if requirements change. This is single reponsobility principle (SRP). A module has one reason to change. A module is not a component a module is a BOUNDARY. The whole folder is one module: 
- responsibility: billing
- reasons to change: pricing/payment rules
- public API: exported functions form index.ts

```
b/
 └── billing/
     ├── stripe.ts
     ├── plans.ts
        └── index.ts

``` 
