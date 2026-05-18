# Cross-Trade Safety-First Intake Ordering

The single most important question to ask any AI answering service vendor: what happens on a gas-smell call?

## The wrong order (what most generic AI scripts do)

1. Capture caller name
2. Capture phone number
3. Capture address
4. Ask what the issue is
5. Maybe escalate if gas-smell mentioned

This loses ~30-60 seconds while the home is filling with gas.

## The right order (what configured contractor AI ships)

For any safety-sensitive call (gas smell, carbon monoxide alarm, burning smell, visible fire, exposed live wire, active flooding above electrical):

1. **Detect safety signal in first 5-10 seconds of the call.**
2. **Tell caller to leave the home and call 911 or utility BEFORE asking any commercial intake question.**
3. **Stay on the line until the caller confirms they are at a safe location.**
4. **Once safe, capture intake.**
5. **Send urgent SMS handoff to on-call tech with the safety state flagged.**

## Per-trade safety triggers

### HVAC
- "I smell gas"
- "My carbon monoxide detector is going off"
- "My furnace is smoking"
- "I smell something burning from the vents"

### Plumbing
- "I smell gas from the water heater"
- "Water is pouring near electrical outlets"
- "Sewage is backing up into the bathroom"

### Electrical
- "My electrical panel is sparking"
- "There's a burning smell from the outlet"
- "I see flames coming out of the outlet"
- "Exposed wires after a storm"
- "GFCI keeps tripping and breaker panel is hot"

### Roofing
- "Tree fell on the house and I think it hit the power line"
- "Water is coming through the ceiling near the lights"
- "Active fire from chimney area"

## The SMS handoff packet for safety calls

When the intake completes for a safety-flagged call, the SMS to the on-call tech should include:

- Priority-1 tag (red urgency)
- Caller name + dialable phone number (tap-to-call ready)
- Address with cross-streets
- Problem in caller's own words (verbatim)
- **Safety state**: "home evacuated" / "caller still inside" / "911 called"
- Trade-specific context
- Transcript URL

## Why the order matters

In an actual gas leak, the home is filling with combustible gas at a rate that creates ignition risk within 5-15 minutes depending on home size and leak source. Every wasted second on commercial intake while the caller is still inside the home is risk.

A configured contractor AI ships safety-first ordering by default. Generic AI answering services depend on what you wrote in the intake script. Live operator services depend on the operator on shift and how well they remember the script. Always verify before signing.

## Reference

This page is part of the [contractor-ai-intake-templates](https://github.com/Quirk6/contractor-ai-intake-templates) repo. Originally published as part of the [HVAC 8-point buyer test on oncrew.ai](https://oncrew.ai/blog/how-to-choose-answering-service-hvac-company). CC BY 4.0.
