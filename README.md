# LocalGraf Arc Demo Design Spec

## Objective
- Implement a "recent events" page and an "event" page to demo Arc + LocalGraph
- Build something as production ready as possible to scout future integrations & Arc development

## Context
- **[Content Sources](https://dmn.arcpublishing.com/alc/arc-products/pagebuilder/fusion/documentation/recipes/defining-content-source.md)** are JS modules that fetch data from outside Arc
- **Templates** are Arc Pages with no Content Sources
- **[Resolvers]()** map a user-facing Arc URI to **1)** a Fusion Template and **2)** a Content Source (which fetches data using params in the URI)
    - see locally @ http://localhost/pf/admin/app/tools/resolver-configs.html

## Challenges
- Resolver API is opaque and [poorly documented](https://dmn.arcpublishing.com/alc/answers/464)
- LocalGraf API may change (given future requirements)
- Designs & markup will change

## Demo Implications
"Recent Events" widget is unaffected (static fetch recent query doesn't rely on resolver).

Event Pages will be _probably_ be generated with Resolvers in production (e.g. an Arc Template housing our React components + a Content Source that queries LocalGraf for an Event).  **We won't know how to implement Resolvers until Arc training.**

We can't make an event and imediately go to `/demo/event/<id>` to see it.  To demo a new event we have to create a new Page in PageBuilder Page using a Custom Field and specifying an `event_id` [in this PageBuilder menu.]()

## Design Proposal