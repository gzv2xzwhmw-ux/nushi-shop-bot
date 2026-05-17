# nushi-shop-bot
Nushi Shop Bot v3

⚠️ Work in progress — closed source. This repo exists as a project marker. Source code is not public.

Discord bot that powers the in-game shop and rank-grant flow for the Nushi gaming community. Bridges Discord ↔ game servers via RCON, hooks into WooCommerce for store credits, and handles Stripe / PayPal payments end-to-end.
Features

Slash commands: /shop, /buy, /balance, /link (discord.js v14, modal-driven purchase confirmation, embed + button shop browser)
Auto-rank assignment via RCON within ~60s of purchase, across TF2 / Rust / Minecraft
WooCommerce store credit checkout alongside Stripe / PayPal
Retry queue gracefully handles offline game servers
Rank-expiration cron job for time-limited ranks
/admin stats panel: sales YTD, top buyers, refund tracking
Webhook receivers for Stripe, PayPal, and WooCommerce events

APIs & integrations
LayerAPI / LibraryRuntimeNode.js 18+Chat platformDiscord API via discord.js v14DatabaseMySQL 8 via mysql2 (connection pooling)Game-server bridgeRCON protocol via rcon-client (Source-engine RCON for TF2/Rust; Minecraft RCON)PaymentsStripe API, PayPal APIStore creditsWooCommerce REST API (@woocommerce/woocommerce-rest-api)HTTP serverExpress (webhook ingestion)Schedulingnode-cronConfigdotenv
What's been accomplished

✅ Full scaffolding of the v3 bot — bot.js entry point with dynamic command loader (regular + admin), guild-scoped slash command deployment, graceful shutdown
✅ All four player slash commands implemented: /link, /shop, /buy, /balance
✅ Admin command: /admin stats
✅ Service layer — RCON manager (connection pooling per server), rank service, credit service (WooCommerce), webhook handler (Stripe / PayPal / WooCommerce)
✅ Background jobs — rank-expiration cron, RCON retry queue for offline servers
✅ Database layer — schema (users, items, inventory, transactions, rcon_jobs), pooled connection, migration scripts from v2 → v3
✅ .env.example covering Discord, MySQL, WooCommerce, RCON, Stripe, PayPal config slots

What's next

Wire production Stripe / PayPal / WooCommerce credentials into .env
Configure RCON hosts, ports, and passwords for each game server (TF2 / Rust / Minecraft)
Run schema migrations against the production MySQL instance
Add automated test coverage (currently zero — npm test is a placeholder)
First end-to-end purchase test on staging
Health-check and observability hardening before production cutover

Intentionally out of scope
By design, this build excludes the marketplace and battle-pass features from earlier scoping rounds — focus stays on core shop + RCON rank delivery.
Stack at a glance
Node.js 18+ · discord.js v14 · MySQL2 · Express · node-cron · rcon-client · Stripe · PayPal · WooCommerce REST API
