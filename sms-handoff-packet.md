# On-Call SMS Handoff Packet Structure

When an AI answering service hands off an urgent call to the on-call tech, the SMS packet structure matters. A late or thin packet loses jobs and slows response. A complete packet lets the on-call tech roll with full context.

## Recommended structure

```
[PRIORITY-1] {caller_name} - {phone}
{service_address}, {cross_streets_if_known}

Problem (verbatim): "{problem_in_caller_words}"

Safety state: {evacuated | inside | 911_called | n/a}
Trade context: {trade_specific_fields}

Callback window: {agreed_window}
Recording: {recording_url}
Transcript: {transcript_url}
```

## Why each field matters

- **Urgency tag at the top**: lets the on-call tech triage at a glance vs other notifications
- **Caller name + tap-to-call phone**: enables immediate callback from the SMS
- **Address + cross-streets**: routing accuracy
- **Problem verbatim**: the on-call tech wants the homeowner's own words, not a paraphrase
- **Safety state**: critical for fire-risk and flooding-above-electrical calls
- **Trade-specific context**: HVAC unit type, plumbing shutoff state, electrical panel state, roofing damage type
- **Callback window**: respects the homeowner's stated preference
- **Recording + transcript URLs**: lets the on-call tech listen to tone, hear safety details, capture anything the AI missed

## Anti-patterns to avoid

- **One-line SMS**: "Call John at 555-1234, urgent" — too thin, on-call has to re-intake
- **Wrong priority order**: putting commercial fields above safety state
- **Free-form prose**: "Mrs. Smith called and said there was a leak in her..." — slower to scan than structured fields
- **Multi-step pages**: paging the on-call tech via call-then-page is slower than direct SMS

## Reference

This page is part of the [contractor-ai-intake-templates](https://github.com/Quirk6/contractor-ai-intake-templates) repo. CC BY 4.0.
