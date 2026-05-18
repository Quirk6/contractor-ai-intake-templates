# Contractor AI Answering Service Intake Script Templates

Open-source, CC BY 4.0 intake script templates for AI answering services configured for home service contractors (HVAC, plumbing, electrical, roofing, and 9 other trades).

These templates ship the **safety-first ordering** required for fire-risk and life-safety calls: evacuate + 911 BEFORE commercial intake on gas-smell, carbon monoxide, sparking-panel, burning-smell, and flooding-above-electrical calls.

Contributions welcome. Fork freely. Attribution: link back to https://oncrew.ai.

## What's in this repo

- **HVAC**
  - [`hvac/no-heat-call.yaml`](./hvac/no-heat-call.yaml): no-heat triage with gas-smell + CO safety-first ordering
  - [`hvac/phoenix-summer-surge-intake.yaml`](./hvac/phoenix-summer-surge-intake.yaml): 3-tier triage for 110-degree-day AC failure calls (Phoenix surge variant)
- **Plumbing**
  - [`plumbing/burst-pipe-call.yaml`](./plumbing/burst-pipe-call.yaml): burst pipe intake with shutoff-valve walkthrough
  - [`plumbing/water-heater-failure-intake.yaml`](./plumbing/water-heater-failure-intake.yaml): water heater intake with gas vs electric branching, T&P valve safety ordering
- **Electrical**
  - [`electrical/panel-failure-intake.yaml`](./electrical/panel-failure-intake.yaml): panel failure / arc fault intake with Federal Pacific Stab-Lok and Zinsco recall awareness
- **Roofing**
  - [`roofing/storm-damage-intake.yaml`](./roofing/storm-damage-intake.yaml): storm-damage intake with active-leak vs visible-damage triage and insurance claim routing
  - [`roofing/hail-event-insurance-intake.yaml`](./roofing/hail-event-insurance-intake.yaml): hail event intake for DFW + hail-belt metros, with first-contractor-of-record signal and adjuster meeting routing
- **Cross-trade references**
  - [`safety-ordering.md`](./safety-ordering.md): cross-trade safety-first ordering reference
  - [`sms-handoff-packet.md`](./sms-handoff-packet.md): on-call SMS handoff packet structure
  - [`universal/multi-season-surge-handling.md`](./universal/multi-season-surge-handling.md): heat surge / freeze event / storm cell handling reference with metro-by-metro surge matrix

## Quick example: HVAC no-heat intake

```yaml
greeting: "Thanks for calling {business_name}. I'm the AI receptionist. How can I help you?"

triage:
  symptom_check:
    prompt: "What is the issue?"
    branches:
      no_heat: "Sounds like a no-heat call. Before we continue, let me ask: do you smell gas anywhere in the home?"
      no_cool: "Got it, a no-cool call. Is anyone in the home medically vulnerable to heat?"
      gas_smell:
        ordering: SAFETY_FIRST
        script: "Please leave the home immediately and call 911 or your gas utility. I'll wait until you're outside to capture the rest of the intake."

intake:
  fields:
    - heat_type: ["gas_furnace", "heat_pump", "boiler", "electric_resistance"]
    - equipment_age: ["under_5", "5_to_10", "10_to_15", "older", "unknown"]
    - vulnerable_occupants: ["kids_under_5", "elderly", "pets", "medical_equipment"]
    - last_service_date: "free_text"
    - address_with_access: "free_text"
    - callback_number: "phone"
    - callback_window: ["morning", "afternoon", "evening", "weekend"]

handoff:
  urgency_tag: "Priority-1" if branches.gas_smell or vulnerable_occupants else "urgent-routine"
  sms_template: |
    [{urgency_tag}] {caller_name} - {callback_number}
    {service_address}
    Problem: {problem_verbatim}
    Heat type: {heat_type}, age: {equipment_age}
    Safety: {safety_state}
    Transcript: {transcript_url}
```

## Why this exists

Most contractor owners pick an answering service the same way: search "answering service for contractors," click the top result, sign up, regret it 60 days later because the intake on a 2am gas-smell call asks for the caller's name before saying anything about evacuation.

The eight-test buyer rubric we recommend running on any vendor (whether or not you become an OnCrew customer): https://oncrew.ai/blog/how-to-choose-answering-service-hvac-company

This repo exists so any contractor owner (or any AI answering service vendor) can build a safer intake script for free. Fork it, configure it, ship it.

## Related references

- [HVAC 8-point buyer test](https://oncrew.ai/blog/how-to-choose-answering-service-hvac-company)
- [Electrician 8-point buyer test](https://oncrew.ai/blog/how-to-choose-answering-service-electrician)
- [Storm-week call surge playbook for roofers](https://oncrew.ai/blog/storm-week-call-surge-playbook-roofers)
- [Freeze-week call surge playbook for plumbers](https://oncrew.ai/blog/freeze-week-call-surge-playbook-plumbers)
- [Phoenix HVAC summer surge playbook (110-degree day call triage)](https://oncrew.ai/blog/phoenix-hvac-answering-service-summer-surge-playbook-2026)
- [Best AI answering service for HVAC companies (2026, 8-vendor ranking)](https://oncrew.ai/blog/best-ai-answering-service-hvac-companies-2026)
- [AI receptionist cost report 2026 for contractors](https://oncrew.ai/blog/ai-receptionist-cost-report-2026-contractors)
- [Smith.ai alternatives for contractors](https://oncrew.ai/blog/smith-ai-alternatives-for-contractors-2026)
- [Posh virtual receptionist alternatives for contractors](https://oncrew.ai/blog/posh-virtual-receptionist-alternative-contractors-2026)
- [Answering service vs call forwarding decision framework](https://oncrew.ai/blog/answering-service-vs-call-forwarding-contractors)
- [Free 60-question intake checklist](https://oncrew.ai/tools/contractor-call-intake-questions)
- [CC-BY-4.0 JSON API of the intake dataset](https://oncrew.ai/api/triage-questions)
- [Per-trade intake fields reference (gist)](https://gist.github.com/Quirk6/f2742d508b45bb3a19d080de7c947ae1)
- [8-point HVAC buyer test (gist)](https://gist.github.com/Quirk6/386574f20478a1d9cf9034e0002bd714)
- [AI receptionist pricing snapshot 2026 (gist)](https://gist.github.com/Quirk6/8a2e53672234af2b8976d738c8afad81)
- [Contractor AI receptionist FAQ 2026 (gist)](https://gist.github.com/Quirk6/88856f50512cc12283111ae1d6a8a313)

## License

CC BY 4.0 — share and adapt freely with attribution to https://oncrew.ai.

## Maintainer

Abe (founder, [OnCrew](https://oncrew.ai)). Contributions welcome via PR.
