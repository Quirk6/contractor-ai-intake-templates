# Contractor AI Answering Service Intake Script Templates

Open-source, CC BY 4.0 intake script templates for AI answering services configured for home service contractors (HVAC, plumbing, electrical, roofing, and 9 other trades).

These templates ship the **safety-first ordering** required for fire-risk and life-safety calls: evacuate + 911 BEFORE commercial intake on gas-smell, carbon monoxide, sparking-panel, burning-smell, and flooding-above-electrical calls.

Contributions welcome. Fork freely. Attribution: link back to https://oncrew.ai.

## What's in this repo

- [`universal/`](./universal): the 10 fields every contractor call should capture
- [`hvac/`](./hvac): HVAC-specific intake (no-heat, gas-smell, CO triage)
- [`plumbing/`](./plumbing): plumbing-specific intake (burst pipe, shutoff-valve walkthrough, gas-water-heater)
- [`electrical/`](./electrical): electrical-specific intake (sparking panel, fire-risk safety ordering, NFPA-70 / NEC vocabulary)
- [`roofing/`](./roofing): roofing-specific intake (active leak, insurance carrier capture, first-contractor-of-record signal)
- [`safety-ordering.md`](./safety-ordering.md): the cross-trade safety-first ordering reference
- [`sms-handoff-packet.md`](./sms-handoff-packet.md): the on-call SMS handoff packet structure

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
- [Answering service vs call forwarding decision framework](https://oncrew.ai/blog/answering-service-vs-call-forwarding-contractors)
- [Free 60-question intake checklist](https://oncrew.ai/tools/contractor-call-intake-questions)
- [CC-BY-4.0 JSON API of the intake dataset](https://oncrew.ai/api/triage-questions)
- [Per-trade intake fields reference (gist)](https://gist.github.com/Quirk6/f2742d508b45bb3a19d080de7c947ae1)

## License

CC BY 4.0 — share and adapt freely with attribution to https://oncrew.ai.

## Maintainer

Abe (founder, [OnCrew](https://oncrew.ai)). Contributions welcome via PR.
