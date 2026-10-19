# OmniTask — Visual Application Sitemap & User Navigation Flow (Figma / FigJam Map)

> **Document Type:** Visual System Architecture, Interaction Flow & Sitemap Map  
> **Prepared for:** Aswin (`aswin_bd_24_602`)  
> **Version:** 4.4 Master Architecture  

---

## 🗺️ 1. The Visual Figma Image Sitemap

Here is the complete **Figma / FigJam-style Visual Sitemap & Navigation Flow Diagram** for OmniTask:

![OmniTask Application Sitemap & Navigation Flow Diagram](file:///C:/Users/aswin/.gemini/antigravity/brain/6cef2ef1-8703-4702-a821-ff83bec30558/figma_sitemap_navigation_map_1791265676160.jpg)

---

## 🔍 2. Navigation Architecture Breakdown

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                                 APP SHELL & ROLE MODES                                 │
│         [ 👤 Power User (Dense) | 👵 Senior Mode (AAA Feed) | 🛡️ Caregiver ]           │
└───────────────────────────────────────────┬────────────────────────────────────────────┘
                                            │
   ┌────────────────────┬───────────────────┼────────────────────┬───────────────────┐
   ▼                    ▼                   ▼                    ▼                   ▼
┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐
│  1. CALENDAR     │ │  2. FITNESS      │ │  3. REMINDERS    │ │  4. EXPENSE      │ │  ➕ INGESTION    │
│     AGGREGATOR   │ │     PLANNER      │ │     & HEALTH     │ │     & BUDGET     │ │     MODAL (+)    │
├──────────────────┤ ├──────────────────┤ ├──────────────────┤ ├──────────────────┤ ├──────────────────┤
│ • Month Grid     │ │ • Active Routine │ │ • 💊 Pill Course │ │ • Spend Ledger   │ │ 1. Domain Pick   │
│ • Day Timeline   │ │ • Smart Streaks  │ │ • 💳 Bill Alerts │ │ • Dynamic Burn   │ │ 2. 2-Field Speed │
│ • Daily Outflows │ │ • AI Generator   │ │ • 📅 Appointment │ │ • Category Rollup│ │ 3. Auto-Project  │
│ • Density Dots   │ │ • Exercise Edit  │ │ • ✨ Emoji Habit │ │ • Auto-Link Pool │ │    to Calendar   │
└────────┬─────────┘ └────────┬─────────┘ └────────┬─────────┘ └────────┬─────────┘ └────────┬─────────┘
         │                    │                    │                    │                    │
         └────────────────────┴────────────────────┼────────────────────┴────────────────────┘
                                                   │
                                   ┌───────────────┴───────────────┐
                                   ▼                               ▼
                   ┌───────────────────────────────┐ ┌───────────────────────────────┐
                   │  PILL COURSE & ESCALATION     │ │   BILL ──► EXPENSE AUTO-LINK  │
                   ├───────────────────────────────┤ ├───────────────────────────────┤
                   │ • Day 18/30 Progress Bar      │ │ • User marks Bill "Paid"      │
                   │ • Refill Alert (≤ 5 Days)     │ │ • Auto-creates Expense Record │
                   │ • T=0 (Chime) ──► T+5 (Alarm) │ │ • Recalculates Monthly Burn   │
                   │   ──► T+12 (Caregiver Alert)  │ │ • 5-Sec Reversible Undo Toast │
                   └───────────────┬───────────────┘ └───────────────┬───────────────┘
                                   │                                 │
                                   └────────────────┬────────────────┘
                                                    │
                                   ┌────────────────┴────────────────┐
                                   ▼                                 ▼
                   ┌─────────────────────────────────────────────────────────────────┐
                   │                ✏️ UNIVERSAL EDIT & REWRITE DRAWER                │
                   │  • Modify Past Entries • Cascade Sync Between Linked Objects    │
                   │  • Senior Privacy Pause (1-4h) • Ctrl+Z / Ctrl+Y History Stack  │
                   └─────────────────────────────────────────────────────────────────┘
```

---

## 💡 3. Key Interaction Branches Mapped in the Diagram:

1. **Top-Level Role Selector (Left Branch):**
   - Seamlessly switches the entire UI between **⚡ Power User (4-Split)**, **👵 Senior Mode (Single-Stream AAA)**, and **🛡️ Caregiver Telemetry**.
2. **Global '+' Ingestion Branch (Center-Left):**
   - 3-step progressive disclosure: *Activity Type $\rightarrow$ Details & Schedule $\rightarrow$ Review & Auto-Project to Calendar*.
3. **Pill Course Progress & Escalation Branch (Center-Right):**
   - Maps the lifecycle of a medication from *Start Course $\rightarrow$ Progress Bar $\rightarrow$ Refill Warning $\rightarrow$ Escalation Ladder $\rightarrow$ Completion Milestone*.
4. **Bill-to-Expense Auto-Link Branch (Right):**
   - Connects *Bill Due Alarm $\rightarrow$ Paid Confirmation $\rightarrow$ Automated Ledger Entry $\rightarrow$ Budget Balance Update*.
5. **Universal Edit Drawer (Bottom Span):**
   - Spans across all 4 modules, allowing in-place data rewriting and cascade synchronization.
