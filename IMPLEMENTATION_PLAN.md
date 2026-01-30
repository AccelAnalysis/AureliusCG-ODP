# ACG Automation Stack Implementation Plan

This document outlines the phased implementation roadmap for the Aurelius Capital Group (ACG) Automation Stack. It is based on the Vision Blueprint (January 2026) and serves as the living record of progress.

## Executive Summary
The system is organized into three layers:
1.  **Layer 1: Data & Intelligence (The Moat)** – Property discovery, ownership resolution, screening economics.
2.  **Layer 2: Workflow & Discipline** – Intake gatekeeper, asset briefing, partner routing.
3.  **Layer 3: Relationship & Execution Support** – CRM, stage tracking, attribution/compensation.

## Implementation Roadmap (Phased)

### Phase 1: Discipline MVP
*Focus: Establish one front door, standardized intake, and relationship management to prevent chaos.*

#### Layer 2: Intake Gatekeeper
- [ ] **Data Model**: Define `DealRecord` schema with intake fields, status enums, and reason codes.
- [ ] **Dedupe Logic**: Implement checks for existing addresses/parcels to prevent duplicate records.
- [ ] **Screening Workflow**: Build UI for "Pass/Watch/Reject/Research" decisions with mandatory reason codes.
- [ ] **Audit Trail**: Log all status changes and overrides.

#### Layer 2: Asset Brief Generator
- [ ] **Template V1**: Create a standardized `AssetBrief` schema/interface.
- [ ] **Generation Logic**: Auto-populate brief from `DealRecord` and available Layer 1 data.
- [ ] **Versioning**: Ensure briefs are versioned snapshots, not just live database views.
- [ ] **Verification Checklist**: Implement gating checklist for "Partner Ready" status.

#### Layer 3: Lightweight CRM Core
- [ ] **Owner Clusters**: Create `OwnerCluster` and `Contact` data models separate from Properties.
- [ ] **Relationship Locking**: Implement "Cluster Lock" logic to prevent duplicate outreach.
- [ ] **Touch Tracking**: Build logging for calls/emails with mandatory "Next Step" and "Due Date".
- [ ] **Dashboards**: specific views for "Today's Tasks", "My Deals", and "Owner Clusters".

---

### Phase 2: Intelligence Foundations
*Focus: Integrate data aggregation and basic moat elements.*

#### Layer 1: Property Discovery Engine MVP
- [ ] **Data Ingestion**: Integrate property data API (e.g., Attom, Estated) for raw record retrieval.
- [ ] **Normalization**: Standardize address formatting and property types mapping.
- [ ] **Map Interface**: Upgrade map to support bounds-based searching and filtering.
- [ ] **Queues**: Create work queues for Contact, Research, Watchlist, and Discard.

#### Layer 1: Ownership & Entity Resolution MVP
- [ ] **Name Normalization**: Clean and standardize owner string names.
- [ ] **Parcel Linking**: Link properties to parcel IDs.
- [ ] **Basic Clustering**: Group properties by exact owner name/address matches.
- [ ] **Ownership Card**: UI to display resolved owner details and confidence levels.

#### Layer 1: Market NOI Estimation + Motivation Scoring MVP
- [ ] **NOI Banding**: Implement logic for Low/Base/High NOI estimates based on priors.
- [ ] **Motivation Signals**: Ingest basic distress signals (tax, foreclosure, listing history).
- [ ] **Confidence Scoring**: Calculate confidence scores for data completeness.

---

### Phase 3: Conversion Levers
*Focus: Add routing, tracking, and attribution to drive outcomes.*

#### Layer 2: Partner Matching & Routing
- [ ] **Partner Profiles**: Create schema for partner coverage, strengths, and capacity.
- [ ] **Routing Logic**: Implement matching algorithm based on constraints and fit score.
- [ ] **SLA Automation**: Auto-reassign deals if "First Touch" SLA is breached.

#### Layer 3: Execution Stage Tracking
- [ ] **State Machine**: Implement the 9-stage execution flow (Captured -> Closed).
- [ ] **Stage Gates**: Enforce mandatory artifacts before stage transition.
- [ ] **Task Packs**: Auto-generate task lists upon entering specific stages.

#### Layer 3: Attribution & Compensation Logic
- [ ] **Event Ledger**: Create immutable log for attribution events (Source, Relationship, Execution).
- [ ] **Split Calculation**: Implement logic for role floors and point-based splits.
- [ ] **Payouts**: Define logic for close-only payouts.

---

### Phase 4: Moat Compounding
*Focus: Refine with triggers, learning, and advanced features.*

#### Triggers & Watchlists
- [ ] **Event Monitoring**: Listen for changes in external data (liens, listings).
- [ ] **Re-Scoring**: Trigger score updates based on new events.

#### Outcome Learning
- [ ] **Feedback Loop**: Capture reasons for "Pass" vs "Reject" to tune scoring weights.
- [ ] **Priors Update**: Auto-adjust market priors based on realized deal data.

#### Advanced Systems
- [ ] **Milestone Vesting**: Implement phased payout vesting (LOI, PSA, Close).
- [ ] **Dispute Tooling**: workflows for flagging and resolving attribution disputes.
