# Mapping SAML attributes to OpenID Connect claims

This mapping is inspired by an [earlier proposal from REFEDS][whitepaper].

## Standard OIDC claims ##

The following list contains the standard OIDC claims and the corresponding SAML attributes they are filled with.
No mapping is provided for other standard claims not listed here.

  - `sub` <- `pairwise-id` or `subject-id`

    Use either `pairwise-id` or `subject-id`, depending on the OP's policies.
    The `pairwise-id` attribute is, as [defined for SAML][SAML-subject-id], a "pairwise Subject Identifier" in the sense of the [OIDC specification][OIDC] section "8. Subject Identifier Types", meaning that each client will receive a different `sub` value.
    The OP should declare this in its discovery document, because pairwise subject identifier type is not the default.

  - `name` <- `displayName`
  - `given_name` <- `givenName`
  - `family_name` <- `surname`
  - `email` <- `mail`

    Note that `email` is single-valued, while SAML's `mail` isn't.
    If there are more than one value of `mail`, the OP should provide the end user's preferred e-mail address.

[whitepaper]: https://wiki.refeds.org/download/attachments/38895621/20181011-OIDC-WP.pdf?version=2&modificationDate=1539619007924&api=v2 "White Paper for implementation of mappings between SAML 2.0 and OpenID Connect in Research and Education"
[OIDC]: https://openid.net/specs/openid-connect-core-1_0.html "OpenID Connect Core 1.0 incorporating errata set 1"
[SAML-subject-id]: https://docs.oasis-open.org/security/saml-subject-id-attr/v1.0/cs01/saml-subject-id-attr-v1.0-cs01.html "SAML V2.0 Subject Identifier Attributes Profile Version 1.0"
