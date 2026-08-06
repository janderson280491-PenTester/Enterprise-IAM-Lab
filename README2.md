# AndersonTech IAM Lab — Entra ID Module

A hands-on identity and access management lab built to demonstrate practical
Microsoft Entra ID (Azure AD) administration skills, alongside a companion
on-premises Active Directory environment.

This covers the **cloud-native Entra ID portion** of the lab. The
on-premises AD side (OUs, security groups, GPOs) was built separately in
`andersontech.local` and is documented in the `on-prem-ad/` folder of this
repo.

## Why two separate labs instead of one hybrid environment

The original plan was a fully hybrid setup (on-prem AD synced to Entra ID
via Entra Connect). Entra Connect installation was blocked in the
cloud-hosted environment used for this lab, so the two pieces were built and
documented independently instead. Documenting *why* the hybrid sync didn't
happen, rather than hiding it, is intentional — troubleshooting real
environment constraints is itself part of the IAM story.

## What's in this lab

| Area | What was built | Notes |
|---|---|---|
| Users | 50 users created directly in the tenant | Mirrors the department structure from the on-prem AD lab |
| Groups | Static security groups per department (SG-IT, SG-Sales, SG-Executives, etc.) | Assigned membership |
| Licensing | Activated Microsoft Entra ID P2 trial | Unlocked Conditional Access, PIM, and Access Reviews |
| Security Defaults | Disabled | Required to enable Conditional Access — the two are mutually exclusive, since Security Defaults is the free-tier blanket MFA control and Conditional Access is its granular P1/P2 replacement |
| Break-glass account | Dedicated emergency Global Administrator account, excluded from Conditional Access | Standard practice so a misconfigured CA policy can't lock out every admin at once |
| Conditional Access | Policy requiring MFA for the Executives group | Scoped to a sensitive group first, rather than a blanket all-users rule |
| Privileged Identity Management (PIM) | Eligible (not standing) assignment of the User Administrator role | Tested the full eligible → activate → time-limited active cycle |
| Access Reviews | Recurring review of SG-Executives membership, via an Entitlement Management catalog | Demonstrates ongoing governance, not just one-time configuration |

## Licensing notes (worth knowing, not just working around)

Entra ID Free tier does not include Conditional Access, PIM, Access
Reviews, or dynamic group membership — those require P1 or P2. This lab
started on Free tier using the closest equivalent capability at each step
(e.g., Security Defaults instead of Conditional Access) before P2 was
activated. Knowing exactly what each licensing tier unlocks — and that some
features are mutually exclusive across tiers rather than purely additive —
is itself a relevant IAM operations skill.

## Skills demonstrated

- Entra ID tenant administration (users, groups, roles)
- Understanding of Entra ID licensing tiers and their practical implications
- Conditional Access policy design, scoped to risk rather than applied
  blanket, with break-glass account planning
- Privileged Identity Management — just-in-time privileged access instead
  of standing admin rights
- Recurring Access Reviews for ongoing group membership governance
- Environment troubleshooting and clear technical documentation of
  constraints encountered

## Repo structure

```
entra-id/
├── README.md
└── screenshots/
    ├── users-and-groups.png
    ├── conditional-access-policy.png
    ├── break-glass-account.png
    ├── pim-eligible-assignment.png
    ├── pim-activation.png
    └── access-review-setup.png
```
