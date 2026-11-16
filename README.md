# REPORT 2: `INTERVIEW_REPORT.md`
## How I Built Inventory Flow — Project & Process Report

> **Honesty statement:** This project is a **simulated business scenario** built as a resume project. I did not interview real users or observe a real business. All requirements are my own reasoned assumptions, stated as such throughout. AI (an LLM assistant) was used as an engineering mentor and co-planner; every decision below was made or approved by me.

### 1. Project Overview
**Inventory Flow** is an internal inventory & order management system for a simulated medium-sized company (3–5 warehouses, ~100 products, 30–50 orders/day). It replaces a shared Google Sheet with role-based order tracking, per-warehouse stock with reservation, payments with receipts, low-stock alerts, reports, and an audit log.

### 2. My Role and Contribution
I owned the idea, scope, and every decision. I used AI as a structured mentor to walk me through the full software engineering lifecycle, one question at a time, and I accepted, rejected, or modified its recommendations. All 15 lifecycle stages were completed.

### 3. Problem Discovery
I defined the problem myself: order tracking is hard in spreadsheets, there are no low-stock alerts, stock drifts across warehouses, and stock unavailability is discovered late. **These are assumptions, not researched findings** — a limitation I state openly.

### 4. Research and Evidence
**No real-world research was conducted.** I chose a simulated scenario (my explicit decision) rather than interviewing real businesses. No evidence was collected, and none is fabricated in this report.

### 5. Requirement Decisions (and why)
- **Self-registration + Admin approval** — reduces admin workload while keeping control.
- **Admin-only product creation** — avoids duplicate products across warehouses; I explicitly reversed my earlier "warehouse staff add products" idea after considering duplicates.
- **Fixed roles, no runtime permissions** — simpler MVP; I knowingly deferred part of my original "Admin controls per-role actions" idea.
- **Reserved quantity on immediate order creation** — directly prevents overselling, my core pain point.
- **One order = one warehouse** — I chose simplicity over multi-warehouse splitting.
- **Payment records direct, no warehouse confirmation** — for speed/user experience; mistakes handled by cancellation + payment reversal.
- **Returns/refunds excluded** from MVP.
- **Supplier directory only** — I explored product-linked suppliers (Option C), then consciously stepped back to the simpler directory.

### 6. Workflow and Design Decisions
I defined a current workflow (Sales → Google Sheet → phone call to warehouse → dispatch → payment in Sheet + Tally) and an improved one (real-time stock check → system-routed orders → dashboard fulfillment → automatic alerts). I designed the data model collaboratively: 11 entities, with `Stock.reserved_quantity` and `OrderItem.unit_price` (price snapshot) as deliberate correctness choices. APIs were derived from user actions, not invented — 40 endpoints across 10 groups, all role-scoped.

### 7. Technology Decisions
Java + Spring Boot (my existing skill), MySQL, Vite + React + Material UI (my existing skill), JWT auth, and Netlify + Railway deployment (platforms I already knew). I rejected microservices and sockets as unnecessary complexity at this scale. When I didn't understand deployment, I asked, and chose the free-tier path with its sleep limitation accepted.

### 8. AI Usage Disclosure
AI acted as mentor/interviewer, not author. It asked one question at a time, offered options with trade-offs, and flagged weak assumptions (e.g., "no file size limit," "store logs in JSON files," "no supplier records"). I made the calls. AI recommendations I rejected: file-based audit logs, Option C suppliers (reverted), Next.js, sockets, microservices, admin-only cancellation. AI output will be verified through tests and manual end-to-end checks as I build.

### 9. Implementation Log
**Status: planning complete; implementation not yet started at the time of this report.** Planned build order: Foundation → Auth → Users → Products → Stock → Orders → Payments → Notifications → Reports → Suppliers → Audit → Deployment. I will update this section at each milestone with what I built, challenges, and fixes.

### 10. Testing and Validation
**Strategy defined, not yet executed.** JUnit + Mockito unit tests (I am learning JUnit as I build), Spring Boot integration tests including cross-warehouse authorization checks, edge cases (insufficient stock, double cancellation, oversized uploads, expired JWT), light UI tests, and manual walkthroughs of the three key journeys. Nothing will be claimed as working until tested.

### 11. Challenges and Learnings
Key learnings so far: separating "problem" from "solution"; recognizing my own assumptions; the difference between real-time delivery (sockets) and persistent records; why reserved stock prevents overselling; why server-side authorization matters beyond hiding buttons; and the value of deferring complexity (returns, microservices, runtime permissions) honestly rather than pretending it's done.

### 12. What I Would Do Differently
I would do **real user research** (talk to a shop owner or warehouse worker) before finalizing requirements — my biggest honest gap. I would also define the order status-transition matrix earlier.

### 13. Next Steps
Finalize status rules → build and test module by module → deploy to Netlify/Railway → update this report at each milestone → add unit test coverage progressively.

---

Both reports are ready. One reminder: **before uploading `INTERVIEW_REPORT.md`, read it and adjust anything that doesn't yet match reality** — especially sections 9 and 10, which you'll update as you actually build. That's what makes it credible in an interview.
