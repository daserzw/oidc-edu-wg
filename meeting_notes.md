* [20181119 meeting](#20181119)
* [20181205 meeting](#20181205)

# 20181205

OIDF R&E meeting 2018-12-05

Note taker: Davide Vaghetti

## Attendees
* Eric Goodman
* Keith Hazelton
* Nathan Dors
* Davide Vaghetti

## Materials
* REFEDS OIDCre SAML-OIDC White paper
  * https://wiki.refeds.org/display/CON/Consultation%3A+SAML2+and+OIDC+Mappings
* Presentation 
  * http://bit.ly/2QW5D1F

## Agenda
* Welcome & Introduction
  * Davide: this is a kind of "second" kickoff meeting for the APAC timezone, so welcome to everybody.
  * Eric from UCOP. 
    * University of California is 10 to 14 independent entities, each one with its one IdP.
    * OIDC and OAuth2 interest is currently focused on APIs and federated APIs.
	* Also slowly getting some request for federated authentication on OIDC.
  * Nathan from University of Washington.
    * Chairing the OIDC/OAuth Deployment WG.
	  * https://spaces.at.internet2.edu/display/ODWG/OIDC-OAuth+Deployment+Working+Group+Home
	* Member of CACTI group.
	* Interest in API.
  * Keith from University of Wisconsin-Madison and long standing MACE member.
	* Chair of the Internet2 TIER-Data Structures and APIs Working Group.
	  * https://spaces.at.internet2.edu/display/ODWG/OIDC-OAuth+Deployment+Working+Group+Home
    * Interest in OIDC and OAuth2 is related to the work of the APIs WG.
* R&E Claims and scopes specification
  * Start working on the claims specification is a win win because:
	* it should be fairly straight.
	* we already have great content from the work of REFEDS OIDCre:
	  * https://wiki.refeds.org/display/CON/Consultation%3A+SAML2+and+OIDC+Mappings
	* there are a number of OIDC provider used in R&E that are not following any community accepted schema --- interop problems will arise sometime in the future if we do not act now.
	* Nathan notes that the claims specification will also be very useful for the deploy guide for the Shibboleth OIDC Extension that the InCommon oidc-deploy group wants to write.
* Entity Metadata extension specification
  * Nathan asks about the plans?
	* the need for the spec is motivated by our community relying on policy frameworks such as R&S and SIRTFI.
	* Davide: from a technical point of view, a single claim (as in `policy_framework_url`) is not enough why some policy frameworks define additional attributes and not just the adhere-to/support-for tag. Probably a JWT could be used for the purpose.
	* Nathan also notes that we want to be able to track the authority that assigned or verified the tag/policy. Davide: with JWT signing, tracking the issuer should be possible even outside a federation scenario.
    * Davide: to sum up the target is to support both simple tagging as entity category and policy frameworks with additional requirements such as SIRTFI and the CoCo. How much time it will require is directly related to the committment of the contributors.
* R&E Profiles for OIDC:
  * this is by far the most complex specification this WG will work on. Nathan: we should be very clear on the expected outcome and what we want to be covered by the spec.
  * Nathan: the iGOV profile for OIDC is a good model to start with.
  * Nathan: can we rely on the current OIDC Federation standard?
  * Davide: the current OIDC Federation standard recently had a major rewrite, so I would wait a pair of minor releases before consider it stable. 
* Open actions from last meeting
  * Some problems in creating the new github WG in the `openid` namespace will not be available. Not a big deal, for now we'll just use the current one: https://github.com/daserzw/oidc-edu-wg
  * Open the discussion on the claims specification on the mailing list: the action has been postponed until the APAC call has been done. 
* AOB	
  * APAC timezone call: 
    * Davide propose to review the current schedule asking on the list if we need an APAC friendly call.
	* Nathan suggest to just make the APAC call less frequent and everybody agrees it's the best idea.
* Actions:
  * Start a discussion on the mailing list about the claims specification. 
  * Have an initial draft before the next WG Call.
* Next meeting: Dec 17th, 3:00pm UTC.
  
  
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

