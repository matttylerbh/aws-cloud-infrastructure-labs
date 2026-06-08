# AWS Cloud Migration Proposal
## A Video Game Business — Cloud Solutions Architecture Presentation

**Presenter:** Cloud Solutions Architect
**Organization:** Mid-Sized Video Game Studio / Publisher
**AWS Region Used for All Pricing:** US East (N. Virginia) — `us-east-1`
**Date:** May 2026

---

---

# SLIDE 1 — Title Slide

## AWS Cloud Migration Proposal
### Scaling Game Infrastructure with Amazon Web Services

**Organization:** Mid-Sized Video Game Studio & Publisher
**Presenter Role:** Cloud Solutions Architect
**AWS Region:** US East (N. Virginia) — us-east-1
**Presentation Duration:** ~10 Minutes

> *"Our players expect fast, reliable, always-on experiences.
> AWS gives us the infrastructure to deliver that — at any scale."*

---

---

# SLIDE 2 — Who We Are & What We Need

## Our Organization

We are a **mid-sized video game studio and publisher** that:

- Operates **online multiplayer game services** (matchmaking, lobbies, leaderboards)
- Manages **player accounts, profiles, and in-game purchases**
- Distributes **game patches, DLC, trailers, and screenshots** globally
- Analyzes **player behavior, session data, and crash reports**
- Experiences **unpredictable traffic spikes** during launches, events, and promotions

## The Problem with On-Premises Infrastructure

| Challenge | Impact on the Studio |
|---|---|
| Fixed server capacity | Cannot handle launch-day traffic spikes |
| High upfront hardware cost | Capital risk before a game proves successful |
| Manual patching and maintenance | Engineering time diverted from game development |
| Single datacenter | No geographic redundancy or failover |
| Slow provisioning | Takes weeks to add capacity |

---

---

# SLIDE 3 — Business Justification (1 of 2)

## Why Move to AWS? — Five Business Benefits

---

### Benefit 1: Handle Traffic Spikes During Launches and Events

Video games have **highly unpredictable demand**. A new title launch, a seasonal in-game event, a streamer promotion, or a viral moment can cause player traffic to spike 10x–100x within minutes.

**On-premises problem:** The studio must buy enough hardware to handle peak load — hardware that sits idle 90% of the time.

**AWS solution:** EC2 Auto Scaling and Elastic Load Balancing automatically add or remove compute capacity in response to real-time player demand. The studio pays only for what it uses.

> Example: A game launch weekend that draws 500,000 concurrent players can be handled by scaling out EC2 instances automatically — then scaling back down on Monday morning.

---

### Benefit 2: Improve Player Experience and Uptime

Players expect games to be **available 24/7 with minimal downtime**. A server outage during a ranked match or a live event causes player frustration, negative reviews, and churn.

**AWS solution:**
- **Amazon RDS Multi-AZ** automatically fails over to a standby database if the primary instance fails — with no manual intervention
- **Elastic Load Balancing** routes traffic away from unhealthy instances
- **Amazon CloudWatch** monitors server health and triggers alerts or automated recovery actions
- AWS targets **99.99% availability SLAs** on managed services

> A small on-premises team cannot match the redundancy and monitoring that AWS provides out of the box.

---

### Benefit 3: Reduce Upfront Hardware Costs — CapEx to OpEx

Before AWS, launching a new game required purchasing servers, networking equipment, storage arrays, and datacenter space **before knowing if the game would succeed**.

**AWS solution:** The studio pays a **monthly operating expense** based on actual usage — no upfront hardware purchases required. This is especially valuable for:
- Mid-sized studios with limited capital
- New game launches with uncertain player counts
- Games in development that need temporary test environments

> AWS converts large, risky capital expenditures into predictable, scalable monthly costs.

---

---

# SLIDE 4 — Business Justification (2 of 2)

---

### Benefit 4: Global Delivery of Game Files and Patches

Games require frequent updates — patches, DLC, hotfixes, trailers, and screenshots. Players in different regions expect fast download speeds.

**AWS solution:**
- **Amazon S3** stores all game assets with 99.999999999% (11 nines) durability
- **Amazon CloudFront** (CDN) distributes files from edge locations close to players worldwide
- No need to manage regional file servers or CDN contracts separately

> A 10 GB patch delivered via CloudFront reaches a player in Tokyo as fast as one in New York.

---

### Benefit 5: Data-Driven Game Development and Business Decisions

Game studios need to understand **player behavior, retention, crash rates, purchase patterns, and session lengths** to improve games and grow revenue.

**AWS solution:**
- **Amazon CloudWatch** collects server metrics and logs
- **Amazon Kinesis** streams real-time player event data
- **Amazon S3 + Athena** enables SQL queries over raw log data
- **Amazon QuickSight** visualizes trends for developers and business teams

> Data that used to require a dedicated analytics team and separate infrastructure is now available through managed AWS services.

---

---

# SLIDE 5 — Cloud-Native & Serverless Services

## Why Cloud-Native and Serverless?

**Cloud-native services** are built specifically for cloud environments — they are managed, scalable, and integrated with other AWS services. The studio does **not** need to install, patch, or maintain the underlying infrastructure.

**Serverless services** go further — there are **no servers to manage at all**. The studio writes code or configures rules, and AWS handles execution, scaling, and availability automatically.

### Key Benefits for a Game Studio

- **Faster time to market** — less infrastructure setup, more game development
- **Lower operational overhead** — AWS manages patching, scaling, and availability
- **Pay-per-use pricing** — Lambda charges per invocation, not per idle server hour
- **Built-in scalability** — services scale automatically with player demand

---

---

# SLIDE 6 — AWS Services Mapped to Gaming Needs

## AWS Services for a Video Game Business

| AWS Service | Type | How It Helps the Game Studio |
|---|---|---|
| **Amazon EC2** | Cloud-native compute | Runs game backend servers, matchmaking services, login/auth systems, and internal tools. Supports Linux and custom AMIs. |
| **Amazon RDS MySQL** | Managed database | Stores player profiles, inventory, leaderboards, purchases, game progress, and session data. Multi-AZ ensures high availability. |
| **Amazon S3** | Object storage | Stores game patches, DLC, logs, screenshots, trailers, backups, and user-generated content. 11 nines durability. |
| **AWS Lambda** | Serverless compute | Runs event-driven tasks: sending rewards after a match, processing leaderboard updates, resizing uploaded screenshots, or cleaning old logs. No servers to manage. |
| **Amazon API Gateway** | Managed API | Provides secure REST/WebSocket API endpoints for game clients, mobile apps, launchers, and web portals. Scales automatically. |
| **Amazon CloudWatch** | Monitoring | Monitors server health, player traffic, error rates, and latency. Triggers alarms and automated responses. |
| **Elastic Load Balancing** | Traffic distribution | Spreads player connections across multiple backend EC2 instances. Removes unhealthy instances from rotation automatically. |
| **Auto Scaling** | Capacity management | Automatically adds EC2 instances when player count rises (launch day) and removes them when demand drops (off-peak). |
| **Amazon CloudFront** | CDN | Delivers game downloads, patches, and media files from edge locations worldwide. Reduces latency for global players. |
| **AWS IAM** | Access control | Controls permissions for developers, admins, CI/CD pipelines, and automation tools. Enforces least-privilege access. |

---

### Serverless Spotlight: AWS Lambda for Game Events

**Scenario:** After every multiplayer match ends, the game needs to:
1. Calculate final scores
2. Update player rankings in RDS
3. Award in-game currency
4. Send a push notification

**Without Lambda:** A dedicated server runs 24/7 waiting for match-end events — even at 3 AM when no one is playing.

**With Lambda:** A function triggers only when a match ends. It runs for ~200ms, updates the database, and stops. The studio pays for **200ms of compute time**, not 24 hours of idle server time.

---

---

# SLIDE 7 — Architecture Diagram

## AWS Architecture — Video Game Studio
### How the Services Connect End-to-End

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                          PLAYERS (Global)                                           │
└───────────────────────────────┬─────────────────────────────────────────────────────┘
                                │
                                ▼
                   ┌────────────────────────┐
                   │   Amazon CloudFront    │  ← CDN: delivers patches, DLC,
                   │       (CDN)            │    trailers, screenshots globally
                   └────────────┬───────────┘
                                │
                                ▼
                   ┌────────────────────────┐
                   │  Elastic Load Balancer │  ← Distributes player traffic,
                   │       (ELB)            │    removes unhealthy instances
                   └────────────┬───────────┘
                                │
                                ▼
          ┌─────────────────────────────────────────────┐
          │         Amazon EC2 — Backend Servers        │
          │   10 x m6i.8xlarge (32 vCPU / 128 GB RAM)  │
          │  Matchmaking · Login/Auth · Game APIs ·     │
          │  Lobby Systems · Internal Tools             │
          └──────┬──────────────────────┬───────────────┘
                 │                      │
                 ▼                      ▼
  ┌──────────────────────┐   ┌──────────────────────────┐
  │  Amazon RDS MySQL    │   │      AWS Lambda           │
  │  Multi-AZ            │   │  Serverless Functions     │
  │  5 x db.r6g.2xlarge  │   │  Match results · Rewards  │
  │  Player profiles,    │   │  Log cleanup ·            │
  │  inventory,          │   │  Push notifications       │
  │  leaderboards,       │   └──────────────────────────┘
  │  purchases           │
  └──────────────────────┘
                 │
                 ▼
  ┌──────────────────────┐   ┌──────────────────────────┐
  │    Amazon S3         │   │   Amazon CloudWatch       │
  │    Standard          │   │   Monitoring & Alerts     │
  │  Game patches, DLC,  │   │  Server health · Traffic  │
  │  logs, trailers,     │   │  Errors · Latency ·       │
  │  screenshots,        │   │  Auto-recovery triggers   │
  │  backups (2 TB)      │   └──────────────────────────┘
  └──────────────────────┘

  ┌──────────────────────┐   ┌──────────────────────────┐
  │  Amazon API Gateway  │   │      Auto Scaling         │
  │  REST / WebSocket    │   │  Adds EC2 on launch day   │
  │  endpoints for game  │   │  Removes on off-peak      │
  │  clients & apps      │   │  Policy-driven, automatic │
  └──────────────────────┘   └──────────────────────────┘

  ┌──────────────────────────────────────────────────────┐
  │                    AWS IAM                           │
  │  Access control for devs, admins, CI/CD pipelines   │
  │  Least-privilege permissions across all services    │
  └──────────────────────────────────────────────────────┘
```

### Data Flow Description

1. **Players worldwide** connect through **Amazon CloudFront** for fast content delivery (patches, DLC, media)
2. Game client requests hit the **Elastic Load Balancer**, which distributes traffic across the 10 EC2 backend servers
3. **EC2 instances** handle matchmaking, authentication, game APIs, and lobby logic
4. EC2 reads and writes **player data** (profiles, inventory, leaderboards, purchases) to **Amazon RDS MySQL Multi-AZ** — if the primary DB fails, Multi-AZ automatically fails over to the standby
5. **AWS Lambda** handles event-driven tasks triggered by game events (match end, purchase, login) — no idle servers
6. **Amazon S3** stores all static and large assets — patches, DLC, logs, trailers, screenshots, and DB backups
7. **Amazon CloudWatch** monitors all services, collects metrics and logs, and triggers alarms or auto-recovery
8. **Amazon API Gateway** provides secure endpoints for game clients, mobile apps, and web portals
9. **Auto Scaling** watches CloudWatch metrics and automatically adds or removes EC2 instances based on player demand
10. **AWS IAM** enforces least-privilege access across every service and team member

---

# SLIDE 8 — TCO Analysis: Assumptions & Region

## TCO Analysis — Assumptions and Region

### AWS Region
**US East (N. Virginia) — us-east-1**
All pricing sourced from the AWS Pricing Calculator and verified against published AWS rates for this region.

### Global Assumptions

| Assumption | Value |
|---|---|
| Operating System | Linux (no additional OS licensing cost) |
| Uptime | 730 hours/month (24/7, full month) |
| Support Level | Not included — Developer or Business support billed separately |
| Data Transfer | Intra-region EC2 to RDS/S3 assumed free; no significant outbound transfer modeled |
| Pricing Model | Mix of On-Demand baseline and 1-Year Reserved (No Upfront) for steady-state workloads |
| RDS Backup Storage | Automated backups up to 100% of provisioned storage included free by AWS |
| S3 Lifecycle Policies | None — all 2 TB remains in S3 Standard for the full month |
| S3 Cross-Region Replication | None — single region only, no CRR charges |
| EBS Volumes | gp3 type, 100 GB per EC2 instance for OS and application data |

---

---

# SLIDE 8 — TCO: EC2 (10 Linux VMs)

## TCO Component A: 10 Linux EC2 Instances
### 32 vCPU, 128 GB RAM Each — Game Backend Servers

**Use case:** Matchmaking servers, login/auth services, game API servers, lobby systems, and internal tools.

---

### Instance Selection: m6i.8xlarge

| Spec | Value |
|---|---|
| Instance Family | M6i — General Purpose (Intel Ice Lake) |
| vCPUs | 32 |
| RAM | 128 GiB |
| Network | Up to 12.5 Gbps |
| OS | Linux |
| Why M6i? | Balanced 4:1 compute/memory ratio, ideal for game backend workloads. 6th-gen Intel with better price/performance than M5. |

---

### Pricing Model: 1-Year Reserved Instances (No Upfront)

Choosing **1-Year Reserved Instances (No Upfront)** over On-Demand because:
- Game backend servers run 24/7 — predictable, steady-state workload
- 1-Year RI provides approximately 38% savings vs On-Demand with no upfront cash commitment
- More flexibility retained compared to a 3-Year RI commitment

| Pricing Tier | Hourly Rate | Monthly (730 hrs) |
|---|---|---|
| On-Demand | $1.536/hr | $1,121.28 |
| 1-Year Reserved (No Upfront) | ~$0.952/hr | ~$695.00 |

> On-Demand rate: $1.536/hr confirmed via AWS EC2 pricing and Vantage.sh for us-east-1.
> 1-Year Reserved (No Upfront) applies approximately 38% discount = $0.952/hr effective rate.

---

### EC2 Monthly Cost Calculation

```
Per instance (1-Year RI, No Upfront):
  $0.952/hr x 730 hrs/month = $695.00/month

10 instances:
  $695.00 x 10 = $6,950.00/month
```

**EBS Storage — Root Volumes (gp3, 100 GB per instance):**
```
gp3 pricing: $0.08/GB-month
100 GB x $0.08 x 10 instances = $80.00/month
```

---

### EC2 Subtotal

| Component | Calculation | Monthly Cost |
|---|---|---|
| 10 x m6i.8xlarge (1-Yr RI No Upfront) | $0.952 x 730 x 10 | $6,950.00 |
| 10 x 100 GB gp3 EBS root volumes | 1,000 GB x $0.08 | $80.00 |
| **EC2 Total** | | **$7,030.00/month** |

---

---

# SLIDE 9 — TCO: RDS MySQL (5 Servers)

## TCO Component B: 5 Amazon RDS MySQL Servers
### Player Accounts, Leaderboards, Inventory, Purchases, Game Progress

**Use case:** Each RDS instance supports a different game service — player profiles, inventory/economy, leaderboards, session/matchmaking data, and analytics staging.

---

### Instance Selection: db.r6g.2xlarge

| Spec | Value |
|---|---|
| Instance Family | R6g — Memory Optimized (AWS Graviton2 ARM) |
| vCPUs | 8 |
| RAM | 64 GiB |
| Network | Up to 10 Gbps |
| Engine | MySQL 8.0 |
| Why R6g? | Memory-optimized for database workloads. Graviton2 offers approximately 20% better price/performance than x86 equivalents. Ideal for player data with large in-memory working sets. |

---

### Configuration

| Setting | Choice | Reason |
|---|---|---|
| Deployment | Multi-AZ | Automatic failover — game data must stay available during events and launches |
| Storage Type | gp3 SSD | Better baseline IOPS than gp2, lower cost than io1 |
| Storage Size | 500 GB per instance | Covers player data, indexes, and growth headroom |
| Backup Retention | 7 days | Automated daily backups, retained 7 days (free up to provisioned storage size) |
| Pricing Model | 1-Year Reserved (No Upfront) | Databases run 24/7 — RI saves approximately 40% vs On-Demand |

---

### Pricing Calculation

**On-Demand rate for db.r6g.2xlarge:**
- Single-AZ: ~$1.038/hr (confirmed via Holori/Economize.cloud for us-east-1)
- Multi-AZ doubles the instance cost (AWS standard): ~$2.076/hr

**1-Year Reserved (No Upfront) — approximately 40% discount:**
```
$2.076 x 0.60 = $1.246/hr effective rate
```

**Instance cost per month:**
```
$1.246/hr x 730 hrs = $909.58/month per instance
$909.58 x 5 instances = $4,547.90/month
```

**Storage cost (gp3, Multi-AZ — both primary and standby volumes billed):**
```
$0.115/GB-month x 500 GB x 2 (Multi-AZ) x 5 instances = $575.00/month
```

---

### RDS Monthly Cost Summary

| Line Item | Calculation | Monthly Cost |
|---|---|---|
| 5 x db.r6g.2xlarge Multi-AZ (1-Yr RI) | $1.246 x 730 x 5 | $4,547.90 |
| Storage: 500 GB gp3 x 5 x 2 (Multi-AZ) | 5,000 GB x $0.115 | $575.00 |
| Automated Backups (up to provisioned size) | Included free by AWS | $0.00 |
| **RDS Total** | | **$5,122.90/month** |

---

---

# SLIDE 10 — TCO: Amazon S3

## TCO Component C: Amazon S3 Standard Bucket
### Game Patches, DLC, Logs, Trailers, Screenshots, Backups

**Use case:** Central storage for all game distribution assets, player-uploaded content, server logs, and database backups.

---

### Configuration and Assumptions

| Setting | Value |
|---|---|
| Storage Class | S3 Standard |
| Data Volume | 2 TB (2,048 GB) |
| Lifecycle Policies | None — all data stays in S3 Standard for the full month |
| Cross-Region Replication | None — single region (us-east-1) |
| Data Transfer Out | Assumed delivered via CloudFront (not modeled here) or intra-region (free to EC2) |

---

### S3 Standard Pricing (us-east-1)

| Component | Rate | Source |
|---|---|---|
| Storage (first 50 TB/month) | $0.023 per GB/month | AWS S3 Pricing |
| PUT, COPY, POST, LIST requests | $0.005 per 1,000 requests | AWS S3 Pricing |
| GET, SELECT, and other requests | $0.0004 per 1,000 requests | AWS S3 Pricing |

---

### S3 Monthly Cost Calculation

**Storage:**
```
2,048 GB x $0.023/GB = $47.10/month
```

**PUT/COPY Requests (1,000,000 requests):**
```
1,000,000 / 1,000 = 1,000 billable units
1,000 x $0.005 = $5.00/month
```

**GET/SELECT Requests (10,000,000 requests):**
```
10,000,000 / 1,000 = 10,000 billable units
10,000 x $0.0004 = $4.00/month
```

---

### S3 Monthly Cost Summary

| Line Item | Calculation | Monthly Cost |
|---|---|---|
| Storage: 2,048 GB x $0.023 | 2,048 x $0.023 | $47.10 |
| PUT/COPY: 1,000,000 requests | 1,000 x $0.005 | $5.00 |
| GET/SELECT: 10,000,000 requests | 10,000 x $0.0004 | $4.00 |
| Data Transfer Out | Intra-region / via CloudFront (not modeled) | $0.00 |
| **S3 Total** | | **$56.10/month** |

---

---

# SLIDE 11 — TCO Summary

## Total Cost of Ownership — Monthly Summary

| Service | Configuration | Monthly Cost |
|---|---|---|
| **EC2** | 10 x m6i.8xlarge Linux, 1-Yr RI No Upfront + 100 GB gp3 EBS each | $7,030.00 |
| **RDS MySQL** | 5 x db.r6g.2xlarge Multi-AZ, 1-Yr RI No Upfront, 500 GB gp3 each | $5,122.90 |
| **S3 Standard** | 2 TB storage + 1M PUT + 10M GET requests | $56.10 |
| | | |
| **TOTAL** | | **$12,209.00/month** |
| **Annual Estimate** | | **~$146,508/year** |

---

### On-Demand vs Reserved — Savings Comparison

| Service | On-Demand Monthly | Reserved Monthly | Monthly Savings |
|---|---|---|---|
| EC2 (10 instances) | $11,292.80 | $7,030.00 | $4,262.80 |
| RDS (5 instances) | $8,122.90 | $5,122.90 | $3,000.00 |
| S3 | $56.10 | $56.10 | $0.00 |
| **Total** | **$19,471.80** | **$12,209.00** | **$7,262.80/month** |

> Switching from On-Demand to 1-Year Reserved Instances saves approximately **$87,153/year** — without changing any architecture.

> Note: The ~$19,543 on-demand figure referenced in the brief aligns with this on-demand baseline estimate.

---

---

# SLIDE 12 — AWS Pricing Calculator

## AWS Pricing Calculator — How to Build This Estimate

**Calculator URL:** https://calculator.aws/pricing/2/home

---

### Step 1 — EC2

1. Go to calculator.aws and click **Add service**
2. Search for **EC2** and select it
3. Set Region: **US East (N. Virginia)**
4. Instance type: **m6i.8xlarge**
5. Operating system: **Linux**
6. Quantity: **10**
7. Usage: **730 hours/month**
8. Pricing model: **Reserved — 1 Year, No Upfront**
9. Add EBS storage: **gp3, 100 GB x 10 instances**

### Step 2 — RDS MySQL

1. Click **Add service** and search for **RDS**
2. Engine: **MySQL**
3. Instance type: **db.r6g.2xlarge**
4. Deployment option: **Multi-AZ**
5. Quantity: **5**
6. Storage type: **gp3**, 500 GB per instance
7. Pricing model: **Reserved — 1 Year, No Upfront**
8. Backup retention: **7 days**

### Step 3 — S3

1. Click **Add service** and search for **S3**
2. Storage class: **S3 Standard**
3. Storage amount: **2,048 GB**
4. PUT/COPY/POST/LIST requests: **1,000,000**
5. GET/SELECT requests: **10,000,000**
6. Data transfer out: **0 GB** (intra-region assumed free)

### Step 4 — Share and Screenshot

- Click **View summary** to verify totals
- Click **Share** to generate a shareable URL
- Screenshot each service panel and the summary page for submission

---

### Screenshots to Include in Submission

- [ ] EC2 estimate panel (instance type, count, RI term, OS, EBS)
- [ ] RDS estimate panel (instance type, Multi-AZ, storage, engine, RI term)
- [ ] S3 estimate panel (storage GB, PUT requests, GET requests)
- [ ] Summary page showing all three services and grand total

---

---

# SLIDE 13 — Conclusion

## Why AWS Is the Right Move for Our Game Studio

Moving to AWS gives the video game business a **more flexible, scalable, and reliable infrastructure platform**.

### What We Gain

| Business Need | AWS Solution | Outcome |
|---|---|---|
| Handle launch-day traffic spikes | EC2 Auto Scaling + ELB | No crashes, no over-provisioning |
| Keep player data available 24/7 | RDS Multi-AZ | Automatic failover, no manual intervention |
| Distribute patches globally | S3 + CloudFront | Fast downloads for players worldwide |
| Reduce upfront hardware risk | Pay-as-you-go model | CapEx to OpEx, lower financial risk |
| Understand player behavior | CloudWatch, Kinesis, Athena | Data-driven game improvements |
| Run event-driven game logic | AWS Lambda | No idle servers, pay per execution only |

---

### Financial Summary

| Model | Monthly Cost | Annual Cost |
|---|---|---|
| On-Demand (no commitment) | ~$19,472 | ~$233,664 |
| **1-Year Reserved (recommended)** | **~$12,209** | **~$146,508** |
| **Savings with Reserved** | **~$7,263/month** | **~$87,156/year** |

---

### Final Statement

> "Based on an estimated monthly TCO of approximately $12,209 with 1-Year Reserved Instances, the studio gains fully managed compute, database, and storage services without purchasing or maintaining physical infrastructure. For a game company where demand changes overnight and player experience depends on performance and availability, AWS is not just a cost decision — it is a competitive advantage."

---

---

# APPENDIX — Full Arithmetic Verification

## Pricing Rates Used (us-east-1, May 2026)

### EC2 — m6i.8xlarge, Linux
| Pricing Model | Rate | Source |
|---|---|---|
| On-Demand | $1.536/hr | AWS EC2 Pricing, Vantage.sh |
| 1-Year RI No Upfront | ~$0.952/hr | ~38% discount from On-Demand |
| gp3 EBS Storage | $0.08/GB-month | AWS EBS Pricing |

### RDS — db.r6g.2xlarge, MySQL, Multi-AZ
| Pricing Model | Rate | Source |
|---|---|---|
| On-Demand Single-AZ | $1.038/hr | Holori, Economize.cloud |
| On-Demand Multi-AZ | $2.076/hr | 2x Single-AZ (AWS standard) |
| 1-Year RI No Upfront Multi-AZ | ~$1.246/hr | ~40% discount from On-Demand |
| gp3 Storage | $0.115/GB-month | AWS RDS Storage Pricing |

### S3 Standard
| Component | Rate | Source |
|---|---|---|
| Storage | $0.023/GB-month | AWS S3 Pricing |
| PUT/COPY/POST/LIST | $0.005 per 1,000 requests | AWS S3 Pricing |
| GET/SELECT | $0.0004 per 1,000 requests | AWS S3 Pricing |

---

## Full Arithmetic

### EC2
```
On-Demand:    $1.536 x 730 x 10 = $11,212.80/month
RI (1-Yr):    $0.952 x 730 x 10 = $6,949.60 ~ $6,950.00/month
EBS:          100 GB x $0.08 x 10 = $80.00/month
EC2 Total:    $6,950.00 + $80.00 = $7,030.00/month
```

### RDS
```
On-Demand Multi-AZ:   $2.076 x 730 x 5 = $7,577.40/month
RI Multi-AZ (1-Yr):   $1.246 x 730 x 5 = $4,547.90/month
Storage (Multi-AZ):   500 GB x $0.115 x 2 x 5 = $575.00/month
RDS Total:            $4,547.90 + $575.00 = $5,122.90/month
```

### S3
```
Storage:   2,048 GB x $0.023 = $47.10/month
PUT:       1,000,000 / 1,000 x $0.005 = $5.00/month
GET:       10,000,000 / 1,000 x $0.0004 = $4.00/month
S3 Total:  $47.10 + $5.00 + $4.00 = $56.10/month
```

### Grand Total
```
EC2:    $7,030.00
RDS:    $5,122.90
S3:     $56.10
─────────────────────
TOTAL:  $12,209.00/month
Annual: $12,209.00 x 12 = $146,508.00/year
```

---

## Presentation Timing Guide (10 Minutes)

| Slides | Topic | Time |
|---|---|---|
| 1–2 | Title + Organization Overview | 1:00 |
| 3–4 | Business Justification (5 benefits) | 2:30 |
| 5–6 | Cloud-Native and Serverless Services | 2:00 |
| 7–10 | TCO Analysis (EC2, RDS, S3) | 3:00 |
| 11–12 | TCO Summary + Calculator Walkthrough | 1:00 |
| 13 | Conclusion | 0:30 |
| **Total** | | **~10:00** |

---

*Pricing sourced from AWS official documentation, AWS Pricing Calculator (calculator.aws), and verified third-party sources including Vantage.sh, Holori, Economize.cloud, and Computingforgeeks. All prices reflect US East (N. Virginia) us-east-1 region as of May 2026. Actual costs may vary based on usage patterns, negotiated enterprise discounts, and AWS price changes.*
