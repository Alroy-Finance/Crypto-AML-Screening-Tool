**Overview**  
This project implements a rule-based AML (Anti-Money Laundering) screening tool for cryptocurrency transactions, simulating the core compliance workflow used by regulated crypto exchanges and VASPs (Virtual Asset Service Providers).
It screens wallet addresses against a sanctions watchlist, applies typology-based detection rules, and generates a risk-scored compliance report — built to mirror real-world crypto AML monitoring used in regulated digital asset firms.

**Objectives**  
Build a wallet screening engine against an OFAC SDN-style sanctions watchlist.
Simulate realistic crypto transaction data across BTC and ETH.
Apply rule-based AML typology detection (sanctions hits, large transactions, structuring, layering, aggregation).
Generate a risk-scored, audit-ready compliance report.
Replicate a simplified version of a crypto exchange's AML monitoring workflow.

**Tools & Technologies**  
Python, Pandas, NumPy, hashlib, datetime

**Key Features**  
Screens 200 simulated transactions against an 11-entry sanctions and internal watchlist.
Covers both BTC (UTXO model) and ETH (account-based model) transaction structures.
Applies 5 rule-based AML typology filters in a single rule engine.
Calculates a weighted risk score and assigns Low / Medium / High / Critical risk levels.
Performs 24-hour transaction velocity analysis to detect layering and aggregation patterns.
Exports a full screened dataset and a flagged-only compliance report as CSV.

**Methodology**  
Load sanctions watchlist (OFAC SDN-style addresses with entity and designation reason).
Generate synthetic transaction dataset (200 transactions, BTC + ETH, randomised amounts and timestamps).
Screen each transaction against the watchlist for direct address matches.
Apply rule engine:
- R1 — Sanctions watchlist hit
- R2 — Large transaction (≥ $10,000 USD, CTR threshold)
- R3 — Structuring band ($3,000–$9,999 USD)
- R4 — High sender velocity within 24h (layering)
- R5 — High receiver velocity within 24h (aggregation)
Score each transaction and assign a risk level.
Export flagged transactions report with full audit trail.

**Sample Output**

AML SCREENING — SUMMARY RESULTS
- Total transactions screened: 200
- Flagged transactions: 47 (23.5%)
- Risk Level Breakdown: Critical: 8 | High: 12 | Medium: 27 | Low: 153

**Key Insights**  
Rule-based layering does not require label data — most AML typologies can be captured through transaction structure (velocity, amount banding, and watchlist matching) alone.
Combining a binary sanctions check with weighted typology scoring produces a more risk-sensitive output than flagging on sanctions hits alone.
BTC's UTXO model and ETH's account-based model require slightly different monitoring logic, particularly around address reuse patterns.
Velocity-based rules (layering/aggregation) catch structuring behaviour that a simple threshold rule would miss.

**Limitations**  
Uses a synthetic transaction dataset rather than live blockchain data.
Sanctions watchlist is a representative sample, not the live OFAC SDN feed.
Risk scoring weights are illustrative and would need calibration against a real compliance framework before production use.
Does not include wallet clustering or blockchain analytics (e.g., Chainalysis-style entity attribution).

**Author**  
Alroy Fernandes  
LinkedIn: linkedin.com/in/alroy-fernandes-ab0335153/
