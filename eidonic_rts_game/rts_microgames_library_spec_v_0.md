# RTS — Microgames Library — Spec v0

> **North Star:** Fast, skill-forward micro-ops (5–10m) that feed expeditions, research, sieges, and festivals. Rotating playlists, agent-curated, with clear rewards and zero pay-to-win.

---

## 1) Rotation & Curation
- **Playlist Cadence:** weekly rotation per realm; special festival spotlights.  
- **Agentic Curation:** EAI selects from library using telemetry (completion time, fail reasons, satisfaction). Avoids repetition; introduces novelty at safe pace.  
- **Difficulty Bands:** Novice, Veteran, Master; bands scale rewards and mechanics density.  
- **Matchmaking:** solo, duo, squad (4). Cross-playable with NPC squads in off-hours.  
- **Anti-Exploit:** seeds per run; objective permutations; decaying patterns; replay diminishing returns.

---

## 2) Reward Philosophy
- **Primary:** research reagents, blueprint fragments, expedition keys, siege tokens.  
- **Secondary:** cosmetics (earned), titles, lore shards.  
- **Never:** raw DPS boosts outside declared contexts; edges remain situational and capped (see Monetization Spec).

---

## 3) Signature Microgames (MVS set)

### 3.1 **Riftshot: Colossus Hunt** *(formerly “Archery Clash” inspiration)*
Physics-based weak-point volleys against colossal anomaly beasts.
- **Loop:** scan → aim/lead → compensate (wind, gravity, law-nodes) → volley.  
- **Weapons:** throwers, javelins, ballista bolts; later cannons/bombs/guns by realm.  
- **Law Nodes:** local modifiers (time dilation pockets, drift winds, entropy eddies).  
- **Team Roles:** spotter (weak-point calls), battery (ammo/logistics), striker (volleys), warder (ward placement).  
- **Win/Fail:** break thresholds within time; collateral damage and FF lower score.  
- **Rewards:** titan ornament shards, siege tokens, research reagents.  
- **Accessibility:** aim assist bands; color-safe weak-point highlights.

### 3.2 **Hex of Command** (Turn-Based Tactics Ops)
Small-squad tactical chess with fog variants and destructible cover.
- **Loop:** plan (2–5 AP) → execute → react.  
- **Traits:** morale, suppression, overwatch, flanking, elevation.  
- **Fog Flavors:** realm-specific (Technomantic, Memory Miasma, etc.).  
- **Variants:** hostage rescue, extract & hold, bounty capture.  
- **Rewards:** discipline milestones (tactics/diplomacy), blueprint fragments.

### 3.3 **Glyphweave Relays** (Puzzle / Systems)
Route power, align runes, stabilize bridges under time/pressure.
- **Loop:** scan graph → rotate/shift → meet target states while hazards tick.  
- **Hazards:** surge waves, shifting tiles, logic parasites.  
- **Co-op:** split boards with shared resources.  
- **Rewards:** crafting specs, lore shards, expedition keys.

### 3.4 **Veilwalk** (Stealth Heist)
Infiltrate anomalies or strongholds with limited tools and noise budgets.
- **Tools:** decoys, scramblers, shadow steps.  
- **Detection:** cone vision, sound maps, anomaly pulses.  
- **Objectives:** data exfil, artifact lift, sabotage.  
- **Rewards:** rare reagents, intel leads, treaty leverage.

### 3.5 **Bulwark Lines** (Defense Engineering)
Our siege-twist microgame in a compact, replayable format.
- **Loop:** plan lanes → place socketed defenses → physics throws → coordinate resupply.  
- **Bosses:** weak-point walkers, tunneling swarms, phasing artillery.  
- **Co-op:** sapper/healer/spotter roles; friendly fire always on with penalties.  
- **Rewards:** defense ornaments, ward blueprints.

### 3.6 **Conductor’s Ring** (Choir Timing)
Rhythm-QTE mini-sim for Titan choir and formation drills.
- **Loop:** pattern learn → ensemble timing → crescendo finishers.  
- **Latency Tolerance:** ±120ms; server reconciles chords.  
- **Rewards:** choir certifications, titan synergy boosts (event-only), anthem cosmetics.

---

## 4) New-to-genre Experiments

### 4.1 **Chrono-Echo Trails**
You pursue **ghosts of future movement**; predict where foes will *have been*.  
- **Mechanic:** anomalies leak future trails; player derives present positions by reasoned backtracking.  
- **Use:** intel training; rewards boost scouting disciplines.

### 4.2 **Treaty Theater**
Negotiation roleplay with real mechanics.
- **Loop:** propose → simulate → reveal hidden clauses → vote.  
- **Outcome:** win by achieving public goals while masking private clauses (or discovering opponent’s).  
- **Rewards:** diplomacy milestones, social ornaments.

### 4.3 **Mycelial Cartography**
Grow a living map by guiding spores through hostile biomes.  
- **Mechanic:** cellular automata garden; choices change resource veins and fast-travel nodes in the shard for a week.  
- **Rewards:** harvesting rights, festival invites.

### 4.4 **Rift-forge Atelier**
Cosmetic crafting as skill game.
- **Loop:** material prep → pattern weave → finish; scoring by timing/consistency.  
- **Outcome:** higher score unlocks rare dyes/patterns; low-stim variant provided.

### 4.5 **Echo Siege (Asymmetric Coach Mode)**
One player as **tactical echo** (coach) with limited pings and slow-time charges guiding three runners through hazards.  
- **Rewards:** mentor SS, coaching cosmetics.

---

## 5) Tech & Netcode Notes
- Deterministic windows for physics challenges; server authoritative for scoring.  
- Seeded procedural variants per run; anti-macro patterns.  
- Low-spec mode for tactics/puzzle; cloud offload optional.

---

## 6) UX & Accessibility
- Session length picker (5 / 8 / 12 minutes).  
- Clear failure reason UI; tip surfacing via Narrator (Guide mode).  
- Color-blind palettes, audio captioning, input remap, aim-assist bands, low/high-stim toggles.

---

## 7) Reward Tables (starter)
- **Riftshot:** titan ornament shards, siege tokens, reagents.  
- **Hex of Command:** blueprint fragments (tactics/diplomacy), lore.  
- **Glyphweave Relays:** crafting specs, expedition keys.  
- **Veilwalk:** rare reagents, intel leads.  
- **Bulwark Lines:** ward blueprints, defense ornaments.  
- **Conductor’s Ring:** choir certs, anthem cosmetics.

---

## 8) Telemetry
- Completion time, fail points, FF incidents, satisfaction, abandonment.  
- Difficulty elasticity targets (aim for 60–75% clear on Novice; 35–55% on Veteran; 15–30% on Master).  
- Rotation fatigue metrics and novelty scoring.

---

## 9) Open Decisions
- Final name for **Riftshot: Colossus Hunt** acceptable?  
- Weekly playlist size (3–5?) and guaranteed slots per realm?  
- Rewards tuning per band; pity counters for rare drops.  
- Coach/Echo permissions in **Echo Siege**.  
- Accessibility defaults for aim-assist & color modes.

---

> **Seal:** *Small games, wide ripples. Let mastery in minutes change the fate of weeks.*

