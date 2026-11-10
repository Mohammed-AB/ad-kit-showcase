# Ad-Kit Workbench: engineering notes

Campaign production involves more than generating a picture. Ad-Kit Workbench connects the brief, bilingual copy, constrained layouts, media review and export.

## System path

~~~mermaid
flowchart LR
  CampaignBrief --> Copy
  Copy --> LayoutChecks
  LayoutChecks --> MediaRequest
  MediaRequest --> DurableReservation
  DurableReservation --> OwnedOutput
  OwnedOutput --> ReviewAndExport
~~~

This diagram describes the demonstrated system boundary, not a production deployment topology.

## Decisions and tradeoffs

### Separate layout from media generation

Reviewable copy and layout checks remain useful without a provider. Real generated media is stored as a separate owned output.

### Treat an uncertain job as spent until reconciled

Durable reservations and dispatch state prevent cancellation from pretending to refund a video request that may already be running.

### Reopen results without regeneration

The saved PNG and MP4 remain available with paid calls disabled, including direct download and a stable paused video preview.

## Review questions

- What evidence demonstrates **separate layout from media generation**, and what would fail without it?
- What evidence demonstrates **treat an uncertain job as spent until reconciled**, and what would fail without it?
- What evidence demonstrates **reopen results without regeneration**, and what would fail without it?

## Verification boundary

Real 1024-pixel image and approximately three-second vertical motion output recorded and persisted. Restart/reopen with paid calls disabled verified. 55 nonpaid checks passed: 15 unit, 22 database, seven renderer and 11 browser checks; builds passed.

The video is generated short motion, not an avatar performance. Avatar generation is unavailable in this demo. It does not publish ads or spend a campaign budget.
