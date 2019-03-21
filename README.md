# LocalGraf + Arc Demo Design Spec

## Objective
- Implement a "recent events" page and an "event" page to demo Arc + LocalGraph
- Build something as production ready as possible to scout Arc development & future integrations

## Context
- **[Content Sources](https://dmn.arcpublishing.com/alc/arc-products/pagebuilder/fusion/documentation/recipes/defining-content-source.md)** are JS modules that fetch data from outside Arc
- **Templates** are Arc Pages with no Content Sources
- **Resolvers** map a user-facing Arc URI to **1)** a Fusion Template and **2)** a Content Source (which fetches data using params in the URI)
    - see locally: http://localhost/pf/admin/app/tools/resolver-configs.html
    - legacy documentation: https://arcpublishing.gitbooks.io/getting-up-and-running-with-arc/content/chapter1/pagebuilder/resolvers.html

## Challenges
- Resolver API is opaque and [poorly documented](https://dmn.arcpublishing.com/alc/answers/464)
- LocalGraf API may change (given future requirements)
- Designs & markup will change

## Demo Implications
"Recent Events" widget is unaffected (static "fetch recent" query doesn't rely on resolver).

Event Pages will be _probably_ be generated with Resolvers in production (e.g. an Arc Template housing our React components + a Content Source that queries LocalGraf for an Event).  **We won't know how to implement Resolvers until Arc training.**

We can't make an event and imediately go to `/demo/event/<id>` to see it.  To demo a new event we have to create a new Page in PageBuilder Page using a Custom Field and specifying an `event_id` in this PageBuilder Page Editor menu:

<img src="https://raw.githubusercontent.com/nigelgilbert/localgraf-demo-design-docs/master/images/Screen%20Shot%202019-03-20%20at%2011.16.15%20PM.png" width="200" />


## Demo Proposal
1. Add event in Arc admin
2. Show the "Recent Events"
3. Create a new Arc Page
    - select Event by `event_id` in PageBuilder
    - refresh
    - new Event Page will now be rendered

## Implementation Notes
- If we implement a LocalGraf Content Source that works in the PageBuilder GUI drag-n-drop, then it'll be trivial to plug into a Resolver later
- data fetching / error handling will occur in a parent container component
- markup / designs will go in pure functional child components
    - max code reuse (markup is separated from logic and can be swapped out later)

<img src="https://raw.githubusercontent.com/nigelgilbert/localgraf-demo-design-docs/master/images/component-diagram.png" width="600" />

## Other Notes
- I am following up on Arc forums for Resolver documentation
- legacy Arc docs: https://arcpublishing.gitbooks.io/getting-up-and-running-with-arc/content/
