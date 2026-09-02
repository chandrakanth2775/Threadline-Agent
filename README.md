📈 Revenue-Growth Agent — Explainable Upsell & Cross-Sell

An AI-powered revenue growth agent that helps merchants increase sales by proposing bounded, explainable upsell/cross-sell offers from an agent-readable catalog, and checking out via Razorpay test-mode APIs.

🔑 Key Features

Agent-readable catalog (catalog_tools.py)
Structured functions (search_catalog, get_product, get_related, check_stock) instead of prose.
Upsell/cross-sell relationships are explicit graph edges — every recommendation is traceable.

Revenue agent (agent.py)
Walks the cart, proposes add-ons with plain-English reasons, and enforces policy limits.

Bounded & Safe

MAX_ADDON_PCT_OF_SUBTOTAL (30%)

MAX_ADDON_ITEMS (2)

MAX_ORDER_VALUE (₹10,000)

Stock checks before offers

Checkout gated by explicit user confirmation

Audit trail (audit.py)
Every proposal, rejection, and checkout outcome logged in JSONL (audit_log.jsonl).
Transparent reporting with AuditTrail.print_trail().

Graceful failure handling  
Mock Razorpay client injects a simulated timeout.
Retries with backoff; failures return status: failed without charging.

🚀 Run Demo
bash
cd agent
python3 main.py
No API keys required — runs against MockRazorpayClient.

🔑 Going Live (Razorpay Test Mode)

bash
pip install razorpay

export RAZORPAY_KEY_ID=rzp_test_xxxxxxxxxxxx
export RAZORPAY_KEY_SECRET=xxxxxxxxxxxxxxxx


python3 main.py

Automatically switches to RealRazorpayClient when keys are present.

📂 Project Structure
Code
agent/

├── data/catalog.json     # Sample merchant catalog (5 SKUs, cross-sell/upsell graph)

├── catalog_tools.py      # Catalog interface (agent-readable tools)

├── agent.py              # RevenueAgent: propose_offers() + checkout()

├── razorpay_client.py    # Real + Mock Razorpay clients, retry helper
├── audit.py              # JSONL audit trail

├── main.py               # End-to-end demo

└── README.md

🌟 Extensions

Conversational in-app checkout (LLM loop + explicit user confirmation).

Campaign orchestrator (aggregate accepted offers into merchant-facing reports).

Swap catalog.json for a live Razorpay merchant catalog feed — no code changes needed.
