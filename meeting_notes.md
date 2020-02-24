* [20200224 meeting](#20200224)
* [20191021 meeting](#20191021)
* [20190812 meeting](#20190812)
* [20190701 meeting](#20190701)
* [20190618 TNC19 meeting](#20190618)
* [20190603 meeting](#20190603)
* [20190506 meeting](#20190506)
* [20190408 meeting](#20190408)
* [20190325 meeting](#20190325)
* [20190311 meeting](#20190311)
* [20190114 meeting](#20190114)
* [20181217 meeting](#20181217)
* [20181205 meeting](#20181205)
* [20181119 meeting](#20181119)

# 20200224

OIDF R&E meeting 2020 February 24th

Note taker: Davide Vaghetti

## Attendees

* Ronald Hedberg
* Nick Roy
* Nicolas Liampotis
* Mischa Salle
* Davide Vaghetti

## Agenda

* Trust Marks

## Discussion

Roland 
* trust marks we already have something like that in SAML in the form 
of Entity Categories. 
* the issue has been raised at techEx.
* NIST trustmark definition is good enough for our use and as a start.

Trustmarks can be used to notify the conformance to a specific profile 
or standard. This type of conformance to the protocol in the OIDC space 
is currently carried on by the Certification program. There is an ongoing
conversation in the OIDF to see if trust marks could be used along the 
certification program.

Nick notes that Kantara might also be interested in trustmarks.

Use cases:
* for the users to show that an RP is compliant with XYZ
* for the OP and the RP for showing (and checking) compliance with XYZ

What trustmarks do we need/want in the R&E sector?
Bear in mind that a trust mark is just a JWT and nothing prevent it to 
expanded if needed (for example security contacts).

Agreed that in the R&E space we do have an outstanding issue about
how to express entity categories in OIDC and trust marks seems to be 
a good solution.
So, how we can develop trust marks to express Entity Categories:
* as a separete specification (too narrow, too often changed)
* expanding the existing specification of each EC:
  * might be a daunting job without a start
  * some examples as appendix of the current OIDC Fed spec could help.

## Actions

* Send a request for comment to the mailing list inviting to propose 
examples on expressing CoCo, R&S and Sirtfi through Trust Marks.  

## References

* OpenID 2.0 to OpenID Connect Migration 1.0
  https://openid.net/specs/openid-connect-migration-1_0.html  
* Gdoc with strawman for an OIDC R&S claims set:
  https://docs.google.com/document/d/1FQcZEUsjRjVxR5X5uii_Ma9adFIe9ER3b4WE-wYo7hU/edit#
* voPerson schema
  https://github.com/voperson/voperson
* WLCG Common JWT Profiles
  https://doi.org/10.5281/zenodo.3460258


# 20191021

OIDF R&E meeting 2019 October 21st

Note taker: Davide Vaghetti

## Attendees

* Chris Philips
* Etienne Dysli Metref
* Keith Hazelton
* Nicolas Liampotis
* Hannah Short
* Davide Vaghetti

## Agenda

* Recap the current state and program next actions.

## Discussion

* Sources for the R&E claims and scopes:
  * eduPerson schema
  * SCHAC 
  * REFEDS R&S EC
  * voPerson schema
  * WLCG Common JWT Profiles

## Actions

* Set out a strawman proposal on the mailing list for an R&S scope.

## References

* OpenID 2.0 to OpenID Connect Migration 1.0
  https://openid.net/specs/openid-connect-migration-1_0.html  
* Gdoc with strawman for an OIDC R&S claims set:
  https://docs.google.com/document/d/1FQcZEUsjRjVxR5X5uii_Ma9adFIe9ER3b4WE-wYo7hU/edit#
* voPerson schema
  https://github.com/voperson/voperson
* WLCG Common JWT Profiles
  https://doi.org/10.5281/zenodo.3460258

# 20190812

OIDF R&E meeting 2019 August 12

Note taker: Davide Vaghetti

## Attendees

* Wolfgang Pempe
* Christos Kanellopoulus
* Mischa Sallé
* Davide Vaghetti

## Agenda

* Continue the discussion on `sub` and use of `scope`.

## Discussion

### Use of "scoped" SAML 2.0 identifiers for the OIDC sub 

The eduPerson/SAML 2.0 scope as the domain of the Organization does not
exist in OpenID Connect. Thus, even if a SAML scoped identifier would be
used to populate the OIDC sub, the domain part of the identifier MUST NOT
be considered alone.
The OIDC `sub` clam MUST always be treated as an indivisible string that
__only__ when combined together with the `iss` can be used as a globally
unique, or omni-directional, identifier.

In short: a SAML 2.0 scoped identifier MAY be used as `sub`, but it MUST be
treated as a plain OIDC `sub`.

### Coexisting with SAML 2.0 and migration scenarios

Both the migration from SAML 2.0 scenario and the coexisting scenario
should be treated in the spec. Given that in the current federation
landscape we have multiple indentifiers it is not possible to exactly
follow the same approach used for OpenID 2.0 to OpenID Connect migration. 

### eduperson_scoped_affiliation claim

Requesting eduperson_scoped_affiliation makes sense only if the
organization domain can be transmitted (and validated).  

## Actions

* Come up with a draft specification as soon as possible --- Davide will
share it by the end of the month.
* Share comparison tables on the different options for the `sub` and the
`scope` --- Mischa, Davide, contribs welcomed!
## References

* OpenID 2.0 to OpenID Connect Migration 1.0
  https://openid.net/specs/openid-connect-migration-1_0.html  
* Gdoc with strawman for an OIDC R&S claims set:
  https://docs.google.com/document/d/1FQcZEUsjRjVxR5X5uii_Ma9adFIe9ER3b4WE-wYo7hU/edit#


# 20190701

OIDF R&E meeting 2019 July 1

Note taker: Davide Vaghetti

## Attendees

* Nicolas Liampotis
* Mischa Sallé
* Keith Hazelton
* Davide Vaghetti

## Agenda

* Build on the fruitful discussion we had at TNC19 on `sub` and use of `scope`.

## Discussion

### OIDC sub and existing SAML 2.0 identifiers

Started summarizing the discussion we had at TNC19 around the `sub`:
* the openid2.0 migration approach.
* the "stuff the SAML 2.0 identifier into the sub" approach.

To compare the two approches we need to better define them, and more
specifically the "openid2.0 migration" one --- see Actions below.

### OIDC Scope and R&S EC

We started from the TNC19 discussion: at TNC19 we thought that
a sensible approach would be to just extend the `profile` scope and use
the `claims_request` to allow for requesting the optional claims such as
the affiliation. But:
* the `claims_request` is optional and not supported by a very popular
client such as `mod_auth_oidc` (Apache).
* many useful use cases can be addressed just by creating an ad hoc scope,
which wouldn't require any modification on the client --- even string-based
structured scopes can be used (see WLCG JWT profile).

Once again, to compare different solutions we need a detailed description
of the implementations.

## Actions

* Technically define the different approaches for the `sub` and the `scopes`
and the use cases. THEN put the solutions in a table to compare them.

## References

* OpenID 2.0 to OpenID Connect Migration 1.0
  https://openid.net/specs/openid-connect-migration-1_0.html
* WLCG Common JWT Profiles
  https://docs.google.com/document/d/1cNm4nBl9ELhExwLxswpxLLNTuz8pT38-b_DewEyEWug


# 20190618

OIDF R&E - TNC19 - meeting 2019 June 18

Note taker: Hannah Short

## Attendees

* Hannah Short
* Roland Hedberg
* Mischa Sallé
* Maarten Kremers
* Chris Philips
* Marcus Hardt
* Wolfgang Pempe
* Mike Jones
* Judith Bush
* Davide Vaghetti

## Agenda

* Go through some of the comments on the short OIDC R&S claims bundle proposal from last meeting:
 https://docs.google.com/document/d/1FQcZEUsjRjVxR5X5uii_Ma9adFIe9ER3b4WE-wYo7hU/edit#

## Discussion

### R&S Bundle for OIDC

Can we define the sub to be the thing we need? Seems to be “No”

Implementors tend to take the ID and use it regardless of attribute definition. We should design for that. 

Input from Mike Jones, “don’t touch sub”, put it in something else, e.g. NameId

Most RP libraries do not expect a scoped sub, would require education of RP library developers

Old identifier is only really needed for linking, for new accounts it doesn’t really matter

Do not shift meanings from one spec to another, do not touch what is there. Recommendation not to use a single dictionary. 

Suggestion from Chris that we totally replicate the eduPerson schema, plus populate OIDC standard claims with the same values, might be the cleanest way to do it

Discussion from Judith, could add a scope

OASIS spec allows you to put principal and scope, concatenated in a sub-claim

Should prioritise RPs 

Could we put possible migration data in the user-info endpoint and not in the profile? Keep the profile simple

We shouldn’t try to force things into an OIDC format

SAML Subject-id suggested for sub, this attribute is not yet used in the SAML wild

Options for identifier

* Scoped, in the sub 
* Add a different claim (e.g. subject-id) that is synonymous with a SAML attribute 

What does Empty mean? 

We don’t get case sensitive subjects in reality (Judith) because it comes from LDAP. Should be realistic. 

127 characters for unique part, 127 part for scope part (SAML subject-id claim in OASIS)

eduperson_ is fated to fail, commercial won’t pick it up

Scopes are potentially hard coded in, be careful. It might be complicated and if clients request unsupported scopes you may get strange errors

Need to be careful not to supply surplus attributes (or request them) to be in line with the R&S framework

We could add non-optional claims to the profile schema 

Azure could potentially do more R&E things if necessary

Balance of user info vs ID token, generally everything goes in user info (even common for information to be in the access token)  

### Claims Request/Scope

Claims requests part of spec but not widely implemented

Structured scope suggested by Torsten 

### Scoping

* why is it needed? 
* generally not very sure
* whatever was used should still be used, there are cases 

### This schema should

* Facilitate migration
* Keep it simple for RPs 
* Provide a predictable and enforceable mapping
* Avoid backporting SAML perspective and logic
* One R&E scope
* Avoid incompatibility with industry 

### Tagging

We need to signal adoption of frameworks somehow  

### Example of OpenID 2.0 to OpenId Connect migration
The OpenID 2.0 to OpenID Connect Migration 1.0 specification at
https://openid.net/specs/openid-connect-migration-1_0.html defines the
“openid2_id” claim to transmit the OpenID 2.0 identifier in an OpenID
Connect response – enabling relying parties to support both protocols at
the same time and to correlate older identifiers with new ones.

## Actions

* Pros/Cons table for unique identifier options 
* Pros/Cons table for scope/claims request/extending profile

## Lost and Found
* Should entity categories be included in metadata or authentication context?
* Suggestion (not necessarily to do…) For the mapping, start with most important SAML claims, e.g. affiliation & entitlement. Do it in a proper OIDC way and register in IANA. 


# 20190603

OIDF R&E meeting 2019 June 3

Note taker: Hannah Short

## Attendees

* Hannah Short
* Davide Vaghetti

## Agenda

* Continue the discussion on the R&E claims and scope specification.

## Discussion

Not a long discussion, being just two we decided to work on a brief document about R&S and the WLCG proposed Identity Token and then share it with the community to get some feedback:

 https://docs.google.com/document/d/1FQcZEUsjRjVxR5X5uii_Ma9adFIe9ER3b4WE-wYo7hU/edit#

## Actions
 Davide: share the doc with the REFEDS OIDCre and OIDF R&E communities.
 
### References

* R&S scope and WLCG Identity Token document
  https://docs.google.com/document/d/1FQcZEUsjRjVxR5X5uii_Ma9adFIe9ER3b4WE-wYo7hU/edit#
* REFEDS OIDCre - White Paper for implementation mappings between SAML 2.0 and OpenID Connect in Research and Education
  https://docs.google.com/document/d/1b-Mlet3Lq7qKLEf1BnHJ4nL1fq-vMe7fzpXyrq2wp08/edit#
* REFEDS message on OIDC eduPerson claims:
  https://lists.refeds.org/sympa/arc/refeds/2019-05/msg00002.html
* WLCG Common JWT Profiles:
  https://docs.google.com/document/d/1cNm4nBl9ELhExwLxswpxLLNTuz8pT38-b_DewEyEWug
* Hannah's presentation:
  https://cernbox.cern.ch/index.php/s/f4HFP24SReWKUGc

# 20190506

OIDF R&E meeting 2019-05-06

Note taker: Davide Vaghetti

## Attendees

* Hannah Short
* Roland Hedberg
* Davide Vaghetti

## Agenda

* Continue the discussion on the R&E claims and scope specification.

## Discussion

As seen on the REFEDS mailing list, people are looking for some advises
on claims' names for eduPerson* related attributes.

Starting from the REFEDS/OIDCre SAML-OIDC mapping white paper, we need to
make it clear what is the nature of the proposed claims, that is:
- Registered claims, for which we have the IANA "JSON Web Token Claims" registry.
- Public claims that need to be defined with collision-resistant name, that is a name defined inside a collision-resistant namespace, such as "Domain Names, Object Identifiers (OIDs)..." [3].
- Private claims that are subject to specific agreements between the
provider and the consumer of the claims themselves.

In doing so we need to consider the need expressed by the WLCG community
to have the shortest possible names for the claims in order to put them
directly in the ID Token.

After some discussion, we decided to follow a dual approach:
- register a subset of claims on the IANA registry, namely those proposed
  by the WLCG WG plus affiliation --- possibly short claim names and values.
- in size constrained environment the all the other eduPerson and SCHAC
  claims can be requested through the userinfo endpoint if needed. As for
  the names we can stay with the names already defined in the REFEDS/OIDCre
  white paper --- that is Private claims --- or go for Public claims
  including a full and formal namespace, but we didn't see much usefulness
  in doing so.
  
We will submit the above considerations also to REFEDS to reach a wider
audience.

### References

* REFEDS message on OIDC eduPerson claims:
  https://lists.refeds.org/sympa/arc/refeds/2019-05/msg00002.html
* WLCG Common JWT Profiles:
  https://docs.google.com/document/d/1cNm4nBl9ELhExwLxswpxLLNTuz8pT38-b_DewEyEWug
* Hannah's presentation:
  https://cernbox.cern.ch/index.php/s/f4HFP24SReWKUGc


# 20190408

OIDF R&E meeting 2019-04-08

Note taker: Davide Vaghetti

## Attendees

* Hannah Short
* Keith Hazelton
* Mischa Sallé
* Davide Vaghetti
* Keith Hazelton
* Wolfgang Pempe
* Nicolas Liampotis
* Craig Voisin

## Agenda

* Welcome and Introduction.
* Hannah Short from CERN will introduce the WLCG Common JWT Profiles
specification:
  https://docs.google.com/document/d/1cNm4nBl9ELhExwLxswpxLLNTuz8pT38-b_DewEyEWug

## Discussion

### The WLCG Common JWT Profiles specification

Hannah gave a very clear presentation on the WLCG use case and the
state of the work. Presentation:

 https://cernbox.cern.ch/index.php/s/f4HFP24SReWKUGc

Craig Voisin, from the Global Alliance for Genomics and Healt (GA4GH),
joined the discussion. Craig told us that the GA4GH AAI is facing similar
use cases and challenges.

The discussion focused on three main points:
- WLCG needs to keep the PII and the authorization information in the
same bearer token to be used with unregistered resource servers.
- use of the `scope` claim to express authorization.
- WLCG introduces two new short claims, `ver` and `group`, with a very
concise syntax and concise values as well. The target is to create and
use very short (and short-lived) token.

### References

WLCG Common JWT Profiles:
 https://docs.google.com/document/d/1cNm4nBl9ELhExwLxswpxLLNTuz8pT38-b_DewEyEWug
Hannah's presentation:
 https://cernbox.cern.ch/index.php/s/f4HFP24SReWKUGc

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

