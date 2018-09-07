# Meeting Notes

* [20180828 meeting](#20180828)
* [20180731 meeting](#20180731)
* [20180718 meeting](#20180718)

# 20180907

* Constantin Sclifos (RENAM)
* Davide Vaghetti (GARR)
* Jule Ziegler (DFN/LRZ)
* Nicolas Liampotis (GRNET/AARC)
* Steffen Klemer (DFN)

## Notes

* Davide summarizes the changes (c.f. https://github.com/daserzw/oidc-edu-wg/commits/master ). No objections.
* Talk about next steps according to https://openid.net/wordpress-content/uploads/2010/01/OpenID_Process_Document_December_2009_Final_Approved.pdf :
 * set the editor of the WG (done);
 * send the proposal to the specs@openid.net mailing list (done);
* The work of this initial group is thereby concluded.

# 20180828

## Participants:

* Davide Vaghetti (GARR)
* Chris Phillips (CANARIE)
* Constantin Sclifos (RENAM)
* David Hübner (DAASI, DARIAH)
* Marcus Hardt (KIT)
* Nathan Dors (University Washington)
* Nicolas Liampotis (GRNET)
* Roland Hedberg (Google, GÉANT, SWAMID, OIDF)
* Steffen Klemer (DFN)

## Notes

* intruduction round
* discussion about PR #18 -- add Federation Operators as anticipated audience. No talk against this. Reservations about the idea to ask for the agreement of FedOps in paragraph 8 which is mentioned in the comment of the PR as this would be very binding and to specific. The idea of this is already covered in the phrase "bodies of international organizations relevant in R&E".

* Discussion about the competing draft to oidc-fed called 'JWT federation' by Andreas Solberg. This could be used for any type of protocol (not only oauth) and simplifies the process. Mostly be getting rid of client registration. This was also discussed at the last OIDF connect a/b telco. Roland: JWT federation should be tested with different styles of federations as the spec is designed with one specific federation model in mind. Should the WG consider multiple OID connect types / profiles or only one? (should 4. Proposed Specifications bullet point #1 be in plural or not?). Davide: "In the very end we should only have one profile." Chris (and others): "There might be multiple use cases." Steffen, Chris and others: "There is still the 'maximum consensus' part that should lead to agreement. It's more important to get the WG going and invite more people".

* We should mentioned JWT Federation in the related work.

* Discussion about federations and authorization to (non-web) REST interfaces, similar to "consent" use case?
* Chris: "multi lateral" is missing in the definition of federation; possible opportunity to differentiate from bi-lateral. Discussion if it should go to section 2 or 3. Agreement to talk about "multi-lateral trust" in sec 3.

* Time frame: 10 days from now to collect more comments until Sep, 7th.
* Next call: Sep, 7th 2pm GMT.


# 20180731

## Participants:
* Davide Vaghetti (GARR)
* Jule Ziegler (LRZ - DFN)
* Jens Jensen (STFC)
* Mischa Sallé (NIKHEF)
* Nick Roy (InCommon)
* Roland Hedberg (Independent)
* Steffen Klemer (DFN)
* Chris Philips (CANARIE CAF/ Chair CACTI-I2)
* Mike Jones  (Microsoft)

## Notes

* Introduction Round
* Chris: "People might expect automatically secured endpoints." -- Mike: "As OIDC is build on OAuth 2.0 you might want to use access tokens (perhaps with scopes). These might be ad-hoc or even generic ones to be defined in the edu WG or any of the existing profiles."
* Chris: "Where are API-access control use cases for authenticated users addressed? (compared to human logins)" -- Mike: "In part in the financial-grade profiles."
* Chris: "Have to think about non-web cases; especially GRID which is using x509 atm. Will stuff like OAuth 2.0 profiles for theses cases be part of the edu WG?" -- Mike: "You should mention the concrete use cases but not just mention OAuth 2.0; this is too large."
* Discussion about OAuth-profiles as part of the WG and doing it sooner or later and/or mentioning them in the charter. ... settling unanimously on a more focussed approach on the OIDC fed idea and later "re-charter' with new/broader goals.
* Davide "What about the non-normative parts? keep them / leave them out?" -- Steffen: "Leave them out as there are many existing communities where this could be done and we might lose people because of the IPR." -- Davide: "We might reach a much broader community." -- Chris: "Full non-normative content in REFEDS/aarc/GÉANT...; but parts and informational stuff under the OIDF umbrella." -- Mike "Anything normative (specifications...) should be in the WG BECAUSE of the IPR. Basically everything you can write conformance-tests for. Non-normative guidance could be in the WG but doesn't has to be protected by IPR." -- Davide: "But we anyway have to make it clear to vendors how edu implementations and use cases look like" -- Mike "You are fine to leave it out of the charter but still do it." -- Chris, Roland "We should concentrate on a good and refined, focussed deliverable." -- rough consensus on leaving the non-normative stuff out of the charta
* discussion about "Where should R&E specific things be discussed? Shall we take it out of the closed communities into the broader OIDF forum?"
* Documentation of processes in OIDF WG: docments linked in mailing list mails. Many are using BitBucket because they first supported OIDC; but everything is fine. Also github.
* Timing: Chris: Think about the holidays in August. Therefor consensus on the current schedule although we see the charter more or less ready. Davide: "Close the discussions/comments 1 week beforce the next VC ~28th, August and decide on the final draft then."

## Next meeting

Doodle poll to select a date for the meeting will close in few days:

 https://doodle.com/poll/dwsmk6xdbn86p3ud

The best candidate for now is the 28th of August at 4:00pm CEST
(2:00pm UTC).
We will send a reminder, and the final date will be communicated on
the oidcre@lists.geant.org mailing list.

# 20180718

## Participants
* Chris Philips
* Christos Knaellopoulos
* Davide Vaghetti
* Elena Torroglosa
* Mischa Sallé
* Wolfgang Pempe

## Notes
* Chris asked about scope being more, such as An Oauth2 Profile for Securing APIs -- conclusion was let's take it to the OIDCre list.
* Plan to have this done by the end of August

### Actions
* send an explicit invitation to REFEDS for endorsing the proposal - desired outcome - more organizations/people endorsing the WG activity lends merit to the work. Point out that being a proposer does not involve any committments to work in the WG.
* Chris+Davide to bring this activity to eduGAIN-SG on next call. Chris to raise with Brook (Chair)
* create a Q&A document about the proposed specifications to both anticipate questions and to get note of the community feedback through the ml.

### Next meetings
* end of july/beginng of August (week of July 30)
* mid to late august.
