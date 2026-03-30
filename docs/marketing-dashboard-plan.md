# Marketing Agency Customer Dashboard Blueprint

## 1) Product Goal
Build a client-facing dashboard where each customer can:
- Track campaign progress in real time.
- View business outcomes (leads, ROAS, CAC, pipeline, revenue-attributed).
- Communicate with account managers.
- Purchase additional services and subscription add-ons.

---

## 2) User Roles

### Client Admin
- Can view all campaigns, invoices, users, and purchase services.

### Client Member
- Can view progress/data but cannot buy services (unless granted billing permission).

### Agency Account Manager
- Manages campaign updates, milestones, reports, recommendations.

### Agency Admin
- Manages products/pricing, permissions, integrations, billing settings.

---

## 3) Core Modules

## A. Progress Tracking
- Campaign status board (Not Started / In Progress / In Review / Complete).
- Milestones with due dates and owners.
- Task checklist with blockers.
- Weekly/monthly update feed.
- File and asset delivery history (creative, ad copy, reports).

### B. Performance Analytics
- KPI tiles: Spend, Impressions, Clicks, Leads, CPL, Revenue, ROAS.
- Channel breakdown: Google Ads, Meta Ads, SEO, Email, Social.
- Date-range comparisons (WoW, MoM, custom).
- Funnel view: Visitors → Leads → Qualified Leads → Customers.
- Goal tracking against monthly targets.

### C. Service Marketplace
- Browse service catalog (SEO package, PPC audit, landing page build, etc.).
- One-time purchases and recurring add-ons.
- Checkout with saved payment method.
- Upsell recommendations based on campaign performance.

### D. Communication & Collaboration
- Comment threads on milestones/reports.
- In-app notifications and email digests.
- Meeting notes and action items.

### E. Billing & Contracts
- Plan overview (current retainer + add-ons).
- Invoice history and payment status.
- Contract documents and renewal reminders.

---

## 4) Suggested Tech Stack (MVP-friendly)
- **Frontend:** Next.js + TypeScript + Tailwind + charting library (Recharts/Chart.js).
- **Backend:** Next.js API routes or NestJS.
- **Database:** PostgreSQL.
- **Auth:** Clerk/Auth0/Supabase Auth with role-based access control.
- **Payments:** Stripe (products, subscriptions, one-time checkout).
- **Data sync:** Scheduled jobs (e.g., cron/queue worker) to pull channel metrics.
- **Hosting:** Vercel (frontend) + managed Postgres.

---

## 5) Recommended Data Model (High-level)
- `users` (id, email, role, agency_id, client_account_id)
- `client_accounts` (id, name, industry, timezone)
- `campaigns` (id, client_account_id, channel, status, budget, start_date, end_date)
- `campaign_milestones` (id, campaign_id, title, status, due_date, owner_id)
- `kpi_daily_snapshots` (id, campaign_id, date, spend, clicks, leads, revenue, roas)
- `service_products` (id, name, type, price, billing_interval, active)
- `orders` (id, client_account_id, product_id, status, amount)
- `subscriptions` (id, client_account_id, stripe_subscription_id, status)
- `invoices` (id, client_account_id, amount, due_date, paid_date)
- `comments` (id, campaign_id, author_id, body)
- `notifications` (id, user_id, type, read_at)

---

## 6) MVP Scope (First 6–8 Weeks)

### Phase 1: Foundation (Week 1–2)
- Multi-tenant auth with RBAC.
- Client list + single client dashboard shell.
- Campaign and milestone CRUD.

### Phase 2: Analytics (Week 3–4)
- Connect 1–2 ad channels.
- Daily KPI ingestion.
- KPI overview cards + trend charts.

### Phase 3: Marketplace & Checkout (Week 5–6)
- Service catalog UI.
- Stripe checkout for one-time services.
- Order history table.

### Phase 4: Launch Readiness (Week 7–8)
- Notifications and reporting polish.
- Security hardening, audit logs, role permissions review.
- Pilot with 2–3 client accounts.

---

## 7) Dashboard Layout Recommendation

### Top Nav
- Dashboard | Campaigns | Reports | Services | Billing | Messages

### Dashboard Home
1. KPI snapshot row.
2. Campaign health section.
3. Milestone timeline.
4. “Recommended services” cards.
5. Recent updates + next meeting info.

---

## 8) Revenue Optimization Ideas
- Trigger service recommendations when metrics dip (e.g., high CPL → conversion optimization service).
- Bundle packages (Starter Growth, Scale, Enterprise).
- Offer quarterly strategy workshops as one-click upsells.
- Add annual prepay discounts for retainers.

---

## 9) Security & Compliance Checklist
- Tenant data isolation.
- Role-based permission guards on every endpoint.
- Encryption at rest + TLS in transit.
- Stripe customer portal for secure payment handling.
- Audit logs for sensitive actions (billing changes, role edits).

---

## 10) Success Metrics
- Client login rate (weekly active client users).
- Report engagement time.
- Add-on attach rate (% clients purchasing extra services).
- Retention/churn impact after dashboard adoption.
- Time saved per account manager.

---

## 11) Next Build Step
Implement a clickable prototype with:
1. Dashboard home with fake KPI data.
2. Campaign list + milestone board.
3. Service catalog + test checkout flow.

After prototype sign-off, start with Phase 1 engineering and a single pilot client.
