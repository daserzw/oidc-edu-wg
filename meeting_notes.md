* [20181119 meeting](#20181119)

# 20181119

OIDF R&E meeting 2018-11-19

Note takers: Steffen, Nick, Chris

## Attendees
* Davide Vagehtti
* Niels van Dijk
* Maarten Kremers
* Mischa Salle
* Christos Kanellopoulos
* David Hübner
* Nicolas Liampotis
* Gabriel Zachmann
* Chris Phillips
* John Bradley
* Nick Roy
* Jule Ziegler
* Roland Hedberg
* Steffen Klemer
* Wolfgang Pempe
* Nathan Dors
* Sara Jeanes
* Alejandro Mendez
* Marcus Hardt

## Materials
* Presentation http://bit.ly/2QW5D1F

## Agenda

* Why we've created a R&E WG in the OIDF?
* Work planning: specifications, schedule, commitment.
  * Easiest target would be OIDC claims and scopes for R&E - mostly done, can be done in parallel with OIDC-Federation
  * Consultation will be done on November 26th
    * Quite a few comments on this consultation - will need to work through these
    * Feedback from TechEx: Implementers guidance would be useful
  * What kind of deliverable is this/should this be?
  * Focus is not conversion from/to SAML - need to agree on a set of claims for R&E space, then we can have a specification, not just a guidance document (the list of mappings)
    * Need to be able to write tests for the claims/scopes (for example regEx)
  * Registering claims/scopes with IANA (scopes is a bit problematic in this perspecive)
    * Claims can be registered by IANA, not scopes (yet!) 
    * Do we need to ask oidc-specs-ab about how to register scopes? Would it be an RFC?
      * If we register claims it should be done as an RFC
    * Only claims that need to be registered are ones inside JWTs (no need to register claims only used on the userinfo endpoint)
    * Claim names are already collision-resistant because there is namespace scoping in the name of the claim (eduPerson, SHAC)
    * Action Item: Someone (Davide?) bring this up on the mailing list for discussion
  * Davide as chair should set direction - what to focus on next?
    * Claims and scopes
    * It makes sense to wait for the OIDC Federation specification to be more stable before addressing the R&E profile for OIDC and the Entity metadata topics.
* WG tools:
  * Meeting agendas
  * Meeting notes
  * Repositories, Wikis, Issue trackers
    * https://github.com/daserzw/oidc-edu-wg (move to OIDC github space) - John Bradley will help with migration, Mike Jones probably knows the most about github
    * Fork and make the fork official
    * Davide volunteers to be an admin in the OID foundation github org and add others with commit rights
    * Use the GitHub issue tracker to collect/manage our topics/workstreams
    * OIDF doesn't care if we use GitHub rather than the OIDF bitbucket
  * Mailing List
    * most work should be done there because of the wide time zone spread
    * http://lists.openid.net/mailman/listinfo/openid-specs-rande
  * Need a notes document linked from the invitations
    * Action item: good idea to ask for a primary note-taker at the beginning of each call
    * Put all the notes on the github repository
* AOB
  * Action item: Nathan proposes Davide to blog on the start of the OIDF R&E WG; circled among Nathan and Davide offline
* Next meeting
  * in 2 weeks at December, 5th, 12am CET
* Suggestion from Call attendees:
  * Roland/Chris: Roland outlined that there's a limitation on languages in play and knowing who is working on what is important --> sounds like you are suggesting a list of implementations and in what language to help gain visibility to who's doing what 

