* [20190325 meeting](#20190325)
* [20190311 meeting](#20190311)
* [20190114 meeting](#20190114)
* [20181217 meeting](#20181217)
* [20181205 meeting](#20181205)
* [20181119 meeting](#20181119)

# 20190325

OIDF R&E meeting 2019-03-25

Note taker: Davide Vaghetti

## Attendees

* Keith Hazelton
* Mischa Sallé
* Roland Hedberg
* Maarten Kremers
* Davide Vaghetti

## Agenda

* Welcome and Introduction.
* Continue the discussion on OIDC R&E claim specification
  * see the [20190311 meeting notes](#20190311).

## Discussion

### OIDC R&E claim specification

There has been en extensive discussion on the use of scopes to request
a set of claims. More specifically the discussion started from the REFEDS
R&S Entity Category [R&S-EC].

[R&S-EC], that specify a neat and useful bundle of attributes to be
released to RPs, is currently targeted to the R&E identity federation
world, and thus SAML 2.0, but the translation into an OIDC scope should be
almost painless as specified in [REFEDS-OIDC-SAML-WP].

Everyone agrees that porting [R&S-EC] to OIDC is useful.

Roland points out that scopes in OIDC do not have any other attached
meaning out of those defined for OAuth 2.0 and set of claims. OTOH SAML
Entity Categories express that an entity belongs-to/support-for
a category, and that is why is authorized to request such attributes.

Everyone agrees that [R&S-EC] belongs-to/support-for meaning has to be
expressed through metadata, while the scope(s) and/or the individual
claims request is just an aspect of the technical implementation. In the
end the OP will make a decision about releasing the claims based on
information that are outside the authentication session (the metadata).

Another point discussed: allow or not to request [R&S-EC] only through
scope, or through claims request as well. [R&S-EC] itself does suggest to
use the minimal set of attributes possible, so we should allow the request
of individual claims as well (NOTE: this can also be accomplished with a
set of scopes that are representing the individual claims).

We also discussed about the identifiers and if what requirements we should
push for in the specification. There has recently been a very interesting
discussion on REFEDS on the consequences of not having adopted timely a
good strategy for identifier expression and generation (the focus is on
eduPerson's eduPersonTargetedID). So, while it is true that OIDC itself
is already clear enough on having only two valid identifiers, the public
and the private sub, we need to add some information on the way these
identifiers are created. 

Finally there has been a quick discussion on how to synthetically
represent the tuple `iss` + `sub`, which is the only way to correctly
create a globally unique identifier out of an `id_token`.
The main use case for that short representation is account linking.

Any URL based representation, such as `iss`+`#`+`sub`, would be
interpreted as... an URL! So, as Roland suggested, the best way to avoid
such ambiguity is to use an non-URL based representation, such as:

`sub`+`!`+`iss`

## Actions

* Continue the discussion on the mailing list.

### References

R&S-EC  https://refeds.org/category/research-and-scholarship
REFEDS-OIDC-SAML-WP https://wiki.refeds.org/display/CON/Consultation%3A+SAML2+and+OIDC+Mappings?preview=/38895621/38895643/20181011-OIDC-WP.pdf


# 20190311

OIDF R&E meeting 2019-03-11

Note taker: Davide Vaghetti

## Attendees

* Keith Hazelton
* Mischa Sallé
* Nathan Dors
* Hannah Short
* Roland Hedberg
* Wolfgang Pempe
* Maarten Kremers
* Davide Vaghetti

## Agenda

* Welcome and Introduction.
* Approval of switching to a biweekly call in the EMEA friendly timezone.
* Start the work on the OIDC R&E claim specification (there is a specific
request from the AARC2 project to prioritize it).
* Continue the discussion on entity metadata extension:
  * see the last meeting notes:
  https://github.com/daserzw/oidc-edu-wg/blob/master/meeting_notes.md

## Discussion

### Switch to a biweekly call in EMEA

Everybody approves the proposal to switch to a biweekly call in the
EMEA friendly timezone. From today on, there will be a call every other
Monday at 3:00pm UTC. The OIDF calendar will be updated accordingly.

### OIDC R&E claim specification

There is a general agreement on NOT to go for registering new public
claims in the IANA JSON Web Token Claims Registry. We will use private
claims unless there is a valid reason for not to do so.


Other specification and documents of interest:
* the OIDCre document on mapping between SAML 2.0 and OIDC:
  * White Paper for implementation of mappings between SAML 2.0 and OpenID
Connect in Research and Education
  * link1: https://wiki.refeds.org/display/CON/Consultation%3A+SAML2+and+OIDC+Mappings?preview=/38895621/38895643/20181011-OIDC-WP.pdf
  * link2: https://docs.google.com/document/d/1b-Mlet3Lq7qKLEf1BnHJ4nL1fq-vMe7fzpXyrq2wp08/edit
* Roland suggests to have also a look at the HEART specification (use of
scopes vs claims):
  * https://openid.net/specs/openid-heart-fhir-oauth2-1_0.html


Davide asks if information related to group membership should be taken into
consideration:
* Hannah says it can intersting for research use cases, also it is
important to be able to express (and track/verify?) the group authority.
* Roland invites to have a look a the recent discussion on the source of
authority for claims and attributes that there has recently been on the
A/B connect ml.


There is a general consensus on evaluate if group information will part
of the spec or not: if the spec appears to grow too much, it will be
split. References:
* AARC G002: https://aarc-project.eu/guidelines/aarc-g002/
* AARC G027: https://doi.org/10.5281/zenodo.2247446
* AARC-I047: https://docs.google.com/document/d/18Me5b63R7GKb_1gDfYH02l2sXr3mCIg_suPRw86Ye7I
* voPerson: https://voperson.org/

Davide propose a use case based approach. There are three main use cases:
* Authentication only with the exchange of a transient ID or no ID at all
(in that case the session ID itself will be enough to track the event on
both side) 
* Release of a persistent identifier.
* Release of a persistent identifier + a set of attributes.


Roland also raises the issue of when and where releasing the claims. Many
people are actually asking for the claims to be released directly with the
id_token, or even with the access_token itself, avoiding a call to the
userinfo endpoint. 
Mischa: "The main reason people want to have 'self-contained' tokens instead 
of using a userinfo or introspection endpoint is performance".

'self-contained' tokens might also be useful when there is the need to re-use 
an access_token for multiple resources, not all under the same administrative
umbrella, and some user claims are needed too.

Actions:
* Davide will start a document with what has been agreed so far:
  * subset of claims extracted from the OIDCre white paper.
  * the above list of use cases.


### Entity metadata extension
The discussion will continue on the mailing list.


# 20190114

OIDF R&E meeting 2019-01-14

Note taker: Davide Vaghetti

## Attendees

* Keith Hazelton
* Mischa Sallé
* Nicolas Liampotis
* Sara Jeanes
* Nathan Dors
* Davide Vaghetti

## Agenda & discussion

* Welcome and Introduction 
* Open actions from last meeting 
  * Continue the discusion on the metadata entity extension.
* Specifications roadmap and workplan: 
  * OIDC R&E claims and scopes 
* TBD
  * OIDC Metadata Entity Extension
    * Davide: let's discuss Wolfgang proposal to use the `contacts`
    claim in the `sub_meta` claim defined by OpenID.Federation.
    Ref: http://lists.openid.net/pipermail/openid-specs-rande/Week-of-Mon-20190114/000025.html
    * Nathan: is the `contacts` in `sub_meta` the same that we were
    speaking about?
    * Davide: I think it is not exactly the same thing, the `contacts`
    in the `sub_meta` is valid only inside an entity_statement,
    it cannot be used in a vanilla metadata JSON for an entity. Anyway,
    it doesn't matter WHERE it is used, we should define the structure
    of this new `contacts` claim in the entity metadata extension spec. 
    * Mischa: `contacts` is ambiguous, we should find a name that does
    not collide with the `contacts` claim in the vanilla metadata. 
    * Keith: why do we not just use a `sirtfiContacts` claim for the
    secuirty/Sirtfi contact?
    * Davide/Nicolas: because we need other contact types, at least
    `technical`, `support` and `administrative`. (see below the
    "Sandbox").
    * Mischa: why we do not create new claims at top-level instead of
    relying on this `metadata_ext` JSON object?
    * Davide: the `metadata_ext` JSON object was sought to provide
    extreme flexibility in adding new claims type, do we need such
    flexibility? (see below the "Sandbox").
    * Everyone: it seems better to keep it as simple as possible and also to
    follow the existing conventions in the other OIDC specifications,
    that is to extend top-level adding new claims.
* AOB 

## Sandbox

Example of `metadata_ext` for an RP metadata
```

{
   "application_type": "web",
   "redirect_uris":
     ["https://client.example.org/callback",
      "https://client.example.org/callback2"],
      
[..]

   "metadata_ext":
     {
       "contacts_x": 
         [ 
           { 
             "type": "security", 
             "ref_uri": "http://refeds.org/metadata/contactType/security", 
             "email": ["cert@example.com"], 
             "tel": [ 
               "BETTER-CALL-SAUL", 
               "BIG-TROUBLE-IN-LITTLE-CHINA" 
             ] 
           }, 
           { 
             "type": "technical", 
             "ref_uri": "https://openid.net/connect/rande/metadata/contact/technical", 
             "email": ["techsupport@university-xy.org"], 
           } 
         ]      
     }
}

```

A separate metadata extension element by which you can auto-define new claims

```
{

[..]

    "metadata_ext":
      {
          "claim_name": [...],
          "claim_meta_uri": "https://openid.net/connect/rande/metadata/claim_name"
      }
```
          

# 20181217

OIDF R&E meeting 2018-12-17

Note taker: Davide Vaghetti

## Attendees
* Keith Hazelton
* Nathan Dors
* Mischa Salle
* Nick Roy
* Wolfgang Pempe

## Agenda & discussion
### Entity Metadata extension specification
Davide: on the need to work ASAP on the OIDC metadata extension, see
* http://lists.openid.net/pipermail/openid-specs-rande/Week-of-Mon-20181210/000019.html
* Two approches: JSON object or individual additional claims.

Example JSON Object (metadata_ext claim) for SIRTFI
```
{
  "issuer":
    "https://server.example.com",
   "authorization_endpoint":
    "https://server.example.com/",

[..]

  "metadata_ext": {
    "type": "not-sure",
    "ref_uri": "https://refeds.org/sirtfi",
    "contact": {
      "email": ["cert@example.com"],
      "tel": [
        "BETTER-CALL-SAUL",
        "BIG-TROUBLE-IN-LITTLE-CHINA"
      ]
    }
  }
}
```
     

Nick, Wolfgang, Mischa: vouch for separate JSON object. Extensibility
point can be very convenient for the future.

Mischa: Some doubts on keeping contact inside the metadata_ext for SIRTFI,
we might need to specify also technical and administrative contact types.

All: Agree with Mischa.

It follows some etherpad sand play to try to find a sufficiently flexible
and meaningful structure. Ending up in the following:

* MULTIPLE JSON Objects
```
{
  "issuer":
    "https://server.example.com",
   "authorization_endpoint":
    "https://server.example.com/",

[..]

  "metadata_ext": {
    ["schema_uri": "https://json-schema.org/schema-name.json",
     "type": "contact",
     "contact": {
      "type": "security",
      "email": ["cert@example.com"],
      "url": "https://security.myorg.org/info";
      "tel": [
        "BETTER-CALL-SAUL",
        "BIG-TROUBLE-IN-LITTLE-CHINA"
    ],
    ["type": "entity-attr",
     "namespace_url": "https://refeds.org/entity-attr/assurance",
     "ref_uri": "https://refeds.org/sirtfi",
     ]
    }
  }
}
```
Mischa: there might be other attributes/claims that we need (out of those specific to policy frameworks and entity categories)

Nick write down a list of attributes to be check:

What's missing? (check it out against the current OIDC standard metadata claims in OpenID.Discovery and OpenID.Registration)

Logo URL (or base64 logo) (OP missing)
Privacy Statement URL
Organization Name
Organization DisplayName
DisplayName
Description
ErrorURL (for OPs)
Entity attributes
Contact types
Contacts (missing for the OP)

(Look in OpenID.Discovery for OPs and OpenID.Registration for RPs)

Davide: we need to define a schema  
Keith: the json-schema [json-schema] standard is promising. Used in API
with some success so far.

## Actions
1. Follow the list above to find out how many and which attributes/claims
we need to create to adequately describe an entity in OIDC.
2. Create a list of claims to fully support R&S, SIRTFI and the CoCo (any
other EC or policy frameworks we need to cover?).
3. Try different metadata_ext claim structure (array of objects, array of
array of objects, etc.) with the claims discovered in 1 and 2.

## Next meeting
* Jan 14th 2019, 3:00pm UTC.

## References
[json-schema] https://json-schema.org/

[OpenID.Discovery] http://openid.net/specs/openid-connect-discovery-1_0.html

[OpenID.Registration] https://openid.net/specs/openid-connect-registration-1_0.html


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

