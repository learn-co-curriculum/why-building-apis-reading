# Why Building Api

## Objectives

  1. Understand the value of providing an API
  2. Understand the design considerations when creating APIs

## Outline

  * Building APIs boils down to two different purposes.
    * Building for external usage (Foursquare API, Github API, etc)
      * Heavily documented
      * Versioning!!
      * Auth, rate control
      * We're not covering this much in this unit
    * Building for internal use
      * Discuss the problem of internal apis and auth. Can't store a key on the client, how to do auth?
      * CORs as a way to stop other domains from using your internal API
      * Not going to cover auth in a major way in this unit
