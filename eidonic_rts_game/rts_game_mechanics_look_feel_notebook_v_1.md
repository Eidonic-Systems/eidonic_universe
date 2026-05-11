# RTS — Game Mechanics & Look/Feel — Design Notebook (v1)

> **North Star:** Top‑down angled RTS with deep agentic simulation, 5–30m micro‑ops feeding week‑scale civics and wars. Friendly fire ON (with penalties). Realm‑specific fog. Everything in cycles.

---

## 0) Technical Decisions (Agent Mode v1)
- **Engine:** **Godot 4.x** (MIT). Reasons: open, portable, fast iteration, integrated nav and GDExtension for C++ hot paths.  
- **Rendering:** Forward+ with clustered lights; DLSS/FSR optional; dynamic resolution on low‑end.  
- **Physics:** Godot Physics 3D + custom deterministic layer for combat windows; lightweight projectile sim.  
- **Netcode:** server‑authoritative; **30Hz sim tick**, client **60 FPS** target; input buffering (80–120ms); snapshot + delta with client‑side interpolation; ENet/QUIC transport.  
- **Lockstep Windows:** critical combat resolved in 100ms windows; reconciliation with small input queues.  
- **AI:** Behavior Trees + GOAP hybrid; Utility AI for selection; influence maps for macro; EKRP prompts restricted by tools; per‑agent memory shards (ring buffers) mirrored server‑side.  
- **Pathfinding:** navmesh + hierarchical sectors; flow‑fields for swarms; local avoidance using RVO.  
- **Data:** Timeseries telemetry (Parquet); graph DB for social/economy; job queue (Redis/RQ).  
- **Hivemind Swarm:** agents sharded into **Hives** with blackboards; rate‑limited tool use; memory fences; council‑governed policy updates.

---

## 1) Camera & Controls (LOCKED)
- **Top‑down angled**, full **pan/rotate/zoom** with smooth inertia; collision‑aware edge pan.  
- **Zoom tiers:** **Tactical** (units/micro), **Operational** (base/logistics), **Strategic** (realm overlays, weather, anomalies).  
- **Comfort presets:** classic RTS, orbit, low‑stim; snap zoom hotkeys; radial build wheel (optional) vs. classic sidebar.

---

## 2) Combat Loop
- **Taxonomy:** line (melee/shield), range (bow/rifle), siege, support (healer/buffer), specialist (saboteur/hacker), flyer, titan‑class.  
- **Counters:** soft RPS via armor types, morale, weather, terrain; counter‑intel agents can obfuscate unit types briefly.  
- **Artifacts (defense‑leaning):** zone wards with shard cooldowns; council‑visible timers.  
- **Friendly fire:** **ON**. Penalties: SS loss → fines → cooldown extension → magistrate review for grief patterns.

---

## 3) Base‑Building & Logistics
- **Modular bases** (industry/defense/culture) with adjacency bonuses; public‑works sockets in cities.  
- **Logistics lanes:** roads/rails/air; convoy escorts; sabotage risk; strategic supply overlays; repair/maintenance sinks.  
- **Land Development:** outposts, castles, ranches, workshops, tradeports, observatories; socketed defenses and perks.

---

## 4) Research = Expeditions & Disciplines
- **No linear rush trees.** Unlocks require **expeditions** (mini‑games) + **discipline milestones** (crafting/diplomacy/scholarship).  
- **Pacing bands:** Tier1 1–2h • Tier2 3–5h • Tier3 6–10h • Tier4 10–16h of **active** play (co‑op shortens via synergy bonuses).

**Initial Mini‑Games**  
- **Physics Archery Clash:** wind/arc/weak‑points; later cannons/bombs/guns.  
- **Turn‑Based Tactics Ops:** grid/hex micro‑battles for 5–10m sessions.  
- **Puzzle Relays:** glyphs, bridges, power reroutes under pressure.

---

## 5) Cycles & Anomalies
- **Everything cycles:** weather, harvests, events, anomalies, festivals.  
- **Naming:** Lore Agents generate/curate (e.g., *Cycle of Torment*, *Age of Iron*, *Anomaly Rift*).  
- **Local Sky (optional):** cosmetic sync to player’s local weather & time; **Shard Weather** drives gameplay modifiers.

---

## 6) Fog of War (Realm‑Dependent)
- **Technomantic Fog:** sensor nets & jamming; countered by scouts/drones.  
- **Memory Miasma:** map forgets unless anchored by beacons/books.  
- **Lawlight:** visibility tied to stabilized laws; anomalies dim until rituals/devices brighten.  
- **Echo Fog:** shows **ghost trails** (past movement), never live positions.  
- **Rule:** each realm has a default fog; events may switch types temporarily.

---

## 7) NPC Agency & Economy
- **Agents with memory:** deeds/trades/harms/rescues logged; factions ally/splinter; grudges form and resolve.  
- **Raids:** NPC squads can queue with humans; loot/pay loop back to sim.  
- **Market rollout:** Launch **0%** participation → **10%** → **25%** with dashboards; **Proceeds Ledgers** on NPC bios show funding (public works, education, charities).

---

## 8) PvP, PvE & Sieges
- **PvE:** anomaly raids, caravan escorts, city defenses, bounty hunts.  
- **PvP:** banded skirmishes, declared sieges, seasonal wars with ceasefires and logistics objectives.  
- **Opt‑in Siege playlists:** physics throws, destructible cover, weak‑point bosses, co‑op roles (sapper/healer/spotter), resupply lanes.  
- **Siege scaling caps (per shard tier):** define attacker/defender caps, unit counts, and objective lanes; **dynamic branching** opens/closes lanes based on population/perf.

---

## 9) Alliance Titan — Convergence (Overview)
- **Training:** alliance votes allocate limited build slots (**Hull/Core/Limbs/Aura/Ultimate**); resource pledges; EAI sims tradeoffs.  
- **Control:** piloted by a **choir** of players; shared ability wheel; rhythm QTEs for ultimates.  
- **Counters:** enemy councils craft **Rift Shackles/Disruption Choirs/Anima Leeches**.

---

## 10) UI/UX & Accessibility
- **Clarity first:** one‑tap safety; build sovereignty; robust ping/command wheel.  
- **Narrator:** **Guide** default; **Guardian** default ON; evolves toward Oracle/Ops.  
- **Low‑stim & High‑stim** presets (particle density, shake, bloom, SFX layering); photosensitivity checks; remappable inputs; high‑contrast UI.

---

## 11) Telemetry & KPIs (mechanics‑specific)
- Friendly‑fire incidents per 1k sessions (target downward trend).  
- Siege success vs. pop balance; dynamic branching efficacy.  
- Expedition completion time bands; fail reasons.  
- Fog type effectiveness (scout value, jamming rates).  
- NPC proceeds distribution and player choice patterns.

---

## 12) Open Toggles (to lock next)
- Realm defaults: which fog per initial realms?  
- Friendly‑fire penalty thresholds (exact SS/fine values).  
- Expedition difficulty bands and loot tables.  
- Siege lane counts per shard tier (T1–T3).  
- Titan slot counts per realm theme.

---

> **Seal:** *Make the small loop sing, the week loop matter, and the world remember what we do within it.*

