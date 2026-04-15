# EverSource Mission Power Module
## System Requirements Specification
## Draft SRS v0.1

### 1. Purpose
This document defines system-level requirements for the EverSource Mission Power Module. It is written to support architecture lock, prototype execution, validation planning, supplier engagement, and procurement-facing technical review.

This document covers a common electrical core and four deployment variants:
- unmanned systems
- sovereign AI and edge compute backup
- unmanned marine systems
- expeditionary and defense-support mission systems

This document is intentionally written in requirement language. Every material claim shall be testable.

---

### 2. Scope
The EverSource Mission Power Module is a modular 48 V class hybrid power unit built around:
- a LiFePO4 battery pack for primary energy storage
- a managed supercapacitor stage for transient support and regenerative absorption
- a protection and control layer for charging, load arbitration, telemetry, and safety
- wired, docked, or regulated external DC source integration

This specification covers:
- system function
- electrical architecture
- charging and source interface
- thermal management
- mechanical packaging
- communications and telemetry
- safety behavior
- application-specific requirements by variant
- verification and acceptance basis

This specification does not define final schematic values, final mechanical dimensions, or supplier-specific part numbers.

---

### 3. System Definition
## 3.1 Product Objective
The system shall provide safe, modular, field-serviceable power for autonomous platforms and sovereign compute systems operating in harsh, remote, or infrastructure-poor environments.

## 3.2 Product Variants
- **Variant A:** Unmanned systems mission module
- **Variant B:** Sovereign AI and edge compute backup module
- **Variant C:** Unmanned marine mission module
- **Variant D:** Expeditionary and defense-support mission module

## 3.3 Requirement Conventions
Each requirement includes:
- **Requirement**
- **Verification**
- **Acceptance**

Verification methods are:
- **I** Inspection
- **A** Analysis
- **T** Test
- **D** Demonstration

---

### 4. System-Level Requirements
#### SYS-001
**Requirement:** The system shall provide a nominal 48 V class DC energy storage and delivery architecture.

**Verification:** I, T

**Acceptance:** Nameplate, wiring architecture, and measured output shall confirm a 48 V class system design.

#### SYS-002
**Requirement:** The system shall use LiFePO4 cells as the primary energy storage chemistry for the common core design.

**Verification:** I

**Acceptance:** Cell documentation and pack build records shall identify LiFePO4 chemistry.

#### SYS-003
**Requirement:** The system shall include a dedicated managed supercapacitor stage for transient load support and regenerative energy absorption.

**Verification:** I, T

**Acceptance:** Hardware inspection shall confirm a distinct supercapacitor subsystem, and transient tests shall demonstrate active participation during peak events.

#### SYS-004
**Requirement:** The system shall support modular deployment across all defined variants without requiring redesign of the core battery management logic.

**Verification:** I, A

**Acceptance:** Variant interface definitions shall reuse the common control architecture with only variant-specific interface and packaging changes.

#### SYS-005
**Requirement:** The system shall default to safe operation on loss of noncritical communications.

**Verification:** T, D

**Acceptance:** Loss of supervisory communications shall not cause uncontrolled discharge, unsafe charge behavior, or unsafe contactor state transitions.

#### SYS-006
**Requirement:** The system shall not depend on cloud connectivity for core protection, charging, or fault handling functions.

**Verification:** I, D

**Acceptance:** Core safety and power functions shall remain available with all external network links disconnected.

---

### 5. Electrical Architecture Requirements
#### ELE-001
**Requirement:** The baseline battery topology shall be 16 series LiFePO4 cells.

**Verification:** I

**Acceptance:** Pack schematic and build records shall show a 16S topology.

#### ELE-002
**Requirement:** The system shall support modular energy configurations spanning 0.5 kWh to 2.0 kWh across product variants.

**Verification:** A, I

**Acceptance:** Design variants and configuration tables shall show support within the stated energy range.

#### ELE-003
**Requirement:** The system shall support continuous output power appropriate to variant configuration within a target range of 300 W to 1.5 kW.

**Verification:** T

**Acceptance:** Thermal and electrical test results shall demonstrate continuous operation at the rated power of the configured variant.

#### ELE-004
**Requirement:** The system shall support short-duration burst power through the managed supercapacitor stage.

**Verification:** T

**Acceptance:** Transient testing shall demonstrate burst support above sustained battery-only capability without control-bus brownout.

#### ELE-005
**Requirement:** The system shall include pack-level overcurrent protection.

**Verification:** I, T

**Acceptance:** Hardware inspection shall confirm the protection element, and overcurrent tests shall verify expected protective action.

#### ELE-006
**Requirement:** The system shall include a service disconnect or equivalent safe isolation method.

**Verification:** I, D

**Acceptance:** The pack shall be isolatable for maintenance using the defined service mechanism.

#### ELE-007
**Requirement:** The system shall include a controlled precharge function for bus connection.

**Verification:** I, T

**Acceptance:** Bus-connection testing shall show controlled inrush and no unsafe contactor or connector behavior.

#### ELE-008
**Requirement:** The supercapacitor stage shall not be connected directly across the main bus without controlled charge and discharge management.

**Verification:** I

**Acceptance:** Schematic review shall show controlled interfacing, balancing, and current-limited connection behavior.

#### ELE-009
**Requirement:** The system shall provide current sensing on the primary battery path.

**Verification:** I, T

**Acceptance:** Telemetry and calibration checks shall confirm primary current measurement over the defined operating range.

#### ELE-010
**Requirement:** The system shall include transient suppression and filtering on external source interfaces.

**Verification:** I, T

**Acceptance:** Interface design review and source disturbance testing shall confirm acceptable behavior under expected input disturbances.

---

### 6. Charging and Source Interface Requirements
#### CHG-001
**Requirement:** The system shall support wired DC charging as the baseline recharge method.

**Verification:** D, T

**Acceptance:** The prototype shall charge through a wired DC interface using the defined charge control path.

#### CHG-002
**Requirement:** The system shall support docked charging for variants where unattended recharge is required.

**Verification:** D, T

**Acceptance:** Docked charging shall be demonstrated with repeatable connection and charge initiation.

#### CHG-003
**Requirement:** The charge controller shall enforce a LiFePO4-appropriate charge profile.

**Verification:** I, T

**Acceptance:** Logged charge behavior shall match the defined charge profile for the selected cells.

#### CHG-004
**Requirement:** The system shall inhibit charging when battery temperature is outside the approved charging range.

**Verification:** T

**Acceptance:** Environmental tests shall show no charge acceptance when the pack is below or above approved charge temperature thresholds.

#### CHG-005
**Requirement:** The system shall support controlled preheat prior to charging when low-temperature recovery is enabled for a given variant.

**Verification:** T, D

**Acceptance:** A cold-soaked pack shall enter a preheat state and only transition to charge when the threshold condition is met.

#### CHG-006
**Requirement:** The system shall support charge-rate limiting based on pack temperature, source capability, and protection rules.

**Verification:** T

**Acceptance:** Charge logs shall show rate adjustment under constrained thermal or source conditions.

#### CHG-007
**Requirement:** The system shall tolerate loss of external source power without unsafe oscillation between charge and discharge states.

**Verification:** T

**Acceptance:** Source-loss testing shall show stable transition behavior and correct state handling.

#### CHG-008
**Requirement:** The expeditionary variant shall support integration with a regulated external source or vehicle-power adapter path where required by deployment.

**Verification:** I, T

**Acceptance:** The defined expeditionary source interface shall be present in the design and function correctly under the required input envelope.

---

### 7. Thermal Management Requirements
#### THM-001
**Requirement:** The system shall monitor battery temperature at locations sufficient to protect the pack during charge, discharge, and storage recovery.

**Verification:** I, T

**Acceptance:** Sensor placement and thermal logs shall show coverage adequate for protective decisions.

#### THM-002
**Requirement:** The system shall monitor temperatures of critical power electronics.

**Verification:** I, T

**Acceptance:** Thermal instrumentation shall include the primary heat-generating conversion and switching elements.

#### THM-003
**Requirement:** The control system shall derate charge or discharge performance when thermal limits are approached.

**Verification:** T

**Acceptance:** Thermal stress tests shall show controlled derating before protective shutdown thresholds are exceeded.

#### THM-004
**Requirement:** The system shall support a cold-preheat mode for variants intended for sub-freezing field operation.

**Verification:** D, T

**Acceptance:** The system shall demonstrate a defined preheat sequence and valid transition back to operational states.

#### THM-005
**Requirement:** The baseline thermal design shall favor passive cooling unless active cooling is justified by verified test data.

**Verification:** I, A

**Acceptance:** The design record shall show passive-first thermal rationale or documented evidence supporting active cooling inclusion.

---

### 8. Mechanical and Environmental Requirements
#### MEC-001
**Requirement:** The system enclosure shall protect internal electrical assemblies from expected handling and mission vibration loads.

**Verification:** T, I

**Acceptance:** Inspection and mechanical screening shall show no structural damage or functional interruption after defined vibration exposure.

#### MEC-002
**Requirement:** Internal cells, busbars, and harnesses shall be mechanically restrained to prevent fatigue, fretting, or motion-induced damage.

**Verification:** I, T

**Acceptance:** Inspection after vibration screening shall show no unacceptable movement, wear, or damage.

#### MEC-003
**Requirement:** The enclosure shall provide a defined ingress-protection target appropriate to the intended variant.

**Verification:** T

**Acceptance:** Environmental screening shall meet the ingress criteria defined for the prototype or field variant.

#### MEC-004
**Requirement:** The service architecture shall allow non-destructive access to defined maintenance points.

**Verification:** D

**Acceptance:** The required service tasks shall be completed without destructive disassembly.

#### MEC-005
**Requirement:** External geometry shall minimize unnecessary snag points, exposed live conductors, and avoidable service hazards.

**Verification:** I

**Acceptance:** Design review shall identify no unresolved geometry-related service hazards.

#### MEC-006
**Requirement:** Materials and finishes shall be selected for the actual duty environment rather than novelty or aesthetic preference.

**Verification:** I, A

**Acceptance:** Material selections shall be traceable to environmental, thermal, electrical, and service rationale.

---

### 9. Communications and Telemetry Requirements
#### COM-001
**Requirement:** The system shall provide CAN as the default machine-to-machine interface for mobile variants.

**Verification:** I, D

**Acceptance:** CAN messaging shall be demonstrable using the documented message set.

#### COM-002
**Requirement:** The system shall provide a local service interface for commissioning and diagnostics.

**Verification:** D

**Acceptance:** A technician shall be able to retrieve status, configuration, and fault information through the service interface.

#### COM-003
**Requirement:** The system shall log pack voltage, pack current, thermal state, supercapacitor state, and fault history.

**Verification:** T, D

**Acceptance:** Retrieved logs shall include the required parameter set with timestamps or sequence markers.

#### COM-004
**Requirement:** The system shall retain fault history sufficient for post-event diagnosis.

**Verification:** T, D

**Acceptance:** After induced faults and restart, the stored fault history shall remain retrievable and interpretable.

#### COM-005
**Requirement:** The system shall remain safe if the service interface is disconnected or unavailable.

**Verification:** T

**Acceptance:** Service-interface loss shall not disable core protective functions or normal operating transitions.

#### COM-006
**Requirement:** The sovereign AI variant shall support local-only supervisory integration without requiring external cloud services.

**Verification:** D

**Acceptance:** Local monitoring and control shall function in a network-isolated environment.

---

### 10. Control and Firmware Requirements
#### CTL-001
**Requirement:** The control system shall implement explicit state handling for boot, standby, mission active, burst assist, docked charge, cold preheat, controlled shutdown, fault-limited, and safe isolation modes.

**Verification:** I, T

**Acceptance:** State-machine review and test logs shall show valid entry, exit, and fault transitions for each required mode.

#### CTL-002
**Requirement:** The control system shall estimate state of charge for the battery pack.

**Verification:** T, A

**Acceptance:** SOC reporting shall remain within the project-defined accuracy target under representative load conditions.

#### CTL-003
**Requirement:** The control system shall estimate or track indicators of battery state of health.

**Verification:** I, T

**Acceptance:** The system shall report defined SOH indicators or degradation proxies as specified in the telemetry set.

#### CTL-004
**Requirement:** Burst support shall be authorized only when supercapacitor state, thermal headroom, and bus conditions permit safe delivery.

**Verification:** T

**Acceptance:** Burst events shall be allowed and denied according to defined control thresholds during test scenarios.

#### CTL-005
**Requirement:** The system shall implement load prioritization and controlled load shedding.

**Verification:** T, D

**Acceptance:** Under induced low-energy or fault conditions, noncritical loads shall be shed before critical loads.

#### CTL-006
**Requirement:** Hazardous faults shall latch until defined recovery conditions are met.

**Verification:** T

**Acceptance:** Fault-injection tests shall show latching behavior and correct recovery rules for defined fault classes.

#### CTL-007
**Requirement:** Firmware updates shall support a controlled maintenance workflow and shall not be required for core safe operation in the field.

**Verification:** I, D

**Acceptance:** Update procedures shall be documented and separable from normal protective function.

---

### 11. Safety Requirements
#### SAF-001
**Requirement:** The system shall provide overvoltage protection for the battery pack and relevant subsystem interfaces.

**Verification:** T

**Acceptance:** Overvoltage conditions shall produce the defined protective action without unsafe damage.

#### SAF-002
**Requirement:** The system shall provide undervoltage protection to prevent battery abuse and unsafe brownout behavior.

**Verification:** T

**Acceptance:** Undervoltage conditions shall result in the defined protective response and load-management behavior.

#### SAF-003
**Requirement:** The system shall provide overcurrent protection for the main power path.

**Verification:** T

**Acceptance:** Main-path overcurrent events shall trigger the defined protective action.

#### SAF-004
**Requirement:** The system shall provide overtemperature protection for the battery pack and critical power electronics.

**Verification:** T

**Acceptance:** Thermal stress tests shall show correct protective response before hazardous temperatures are exceeded.

#### SAF-005
**Requirement:** The system shall classify faults into advisory, degraded operation, mission-limiting, and immediate protective shutdown categories.

**Verification:** I

**Acceptance:** The fault table shall assign each implemented fault to one of the defined categories.

#### SAF-006
**Requirement:** Every implemented fault shall have a trigger condition, detection method, logged identifier, and recovery rule.

**Verification:** I

**Acceptance:** Fault documentation shall be complete for all implemented faults.

#### SAF-007
**Requirement:** The system shall enter a safe isolation or equivalent protective state upon defined hazardous failure conditions.

**Verification:** T, D

**Acceptance:** Hazardous-fault tests shall show transition to the protective isolation state.

---

### 12. Unmanned Systems Variant Requirements
#### UMS-001
**Requirement:** The unmanned systems variant shall support propulsion and actuator transients without collapsing control-electronics supply rails.

**Verification:** T

**Acceptance:** Dynamic load tests shall show control rails remain within allowed limits during representative transient events.

#### UMS-002
**Requirement:** The unmanned systems variant shall support a low-power standby mode for dormant deployment periods.

**Verification:** T

**Acceptance:** Standby current shall meet the variant target established in the design baseline.

#### UMS-003
**Requirement:** Where drivetrain architecture supports it, the unmanned systems variant shall support regenerative energy capture or controlled absorption of back-driven energy.

**Verification:** T, D

**Acceptance:** Drivetrain tests shall show safe handling of regenerative or back-driven events.

#### UMS-004
**Requirement:** The unmanned systems variant shall provide machine-readable status and fault reporting suitable for fleet management.

**Verification:** D

**Acceptance:** The defined status and fault set shall be available over the primary interface.

---

### 13. Sovereign AI and Edge Compute Variant Requirements
#### SOV-001
**Requirement:** The sovereign AI variant shall support short ride-through during external source interruption.

**Verification:** T

**Acceptance:** Source-loss testing shall show uninterrupted support for the required ride-through interval defined by the variant baseline.

#### SOV-002
**Requirement:** The sovereign AI variant shall support controlled shutdown signaling for extended outage events.

**Verification:** D, T

**Acceptance:** Extended-outage testing shall show issuance of the defined shutdown signal and orderly transition to the configured state.

#### SOV-003
**Requirement:** The sovereign AI variant shall prioritize output stability and power quality over maximum transient power delivery.

**Verification:** A, T

**Acceptance:** Design review and output tests shall show that ride-through stability and bus cleanliness govern the configured control priorities.

#### SOV-004
**Requirement:** The sovereign AI variant shall support local logging and local supervisory access in a restricted-network environment.

**Verification:** D

**Acceptance:** All required status, control, and log functions shall be demonstrable without internet access.

#### SOV-005
**Requirement:** The sovereign AI variant shall support a maintenance or bypass mode where integration architecture requires service continuity.

**Verification:** D

**Acceptance:** The defined maintenance workflow shall be demonstrated without unsafe interruption of service procedures.

---

### 14. Marine Variant Requirements
#### MAR-001
**Requirement:** The marine variant shall use corrosion-resistant materials, finishes, connectors, and fastening strategy appropriate to salt-exposed environments.

**Verification:** I, A

**Acceptance:** Material and hardware selections shall be documented and appropriate for salt-exposed marine duty.

#### MAR-002
**Requirement:** The marine variant shall include means to detect or report enclosure humidity, leak, or ingress alarm conditions where the mechanical design permits sensor integration.

**Verification:** I, D

**Acceptance:** The marine design shall include the defined input provisions and alarm reporting behavior.

#### MAR-003
**Requirement:** The marine variant shall segregate propulsion power, navigation and control power, communications power, and auxiliary payload power.

**Verification:** I

**Acceptance:** Power-distribution architecture shall show defined segmentation for the required load classes.

#### MAR-004
**Requirement:** The marine variant shall preserve navigation and communications loads ahead of lower-priority payload loads during low-energy or fault conditions.

**Verification:** T

**Acceptance:** Load-shed testing shall show priority preservation of navigation and communications loads.

#### MAR-005
**Requirement:** The marine variant shall be mechanically designed for vibration, slamming, and condensation exposure consistent with unmanned surface vessel service.

**Verification:** T, A

**Acceptance:** Mechanical validation results shall show no unacceptable damage or loss of function under the defined marine test envelope.

#### MAR-006
**Requirement:** The marine variant shall provide a shore-charge or dock-charge path suitable for repeatable mission turnaround.

**Verification:** D, T

**Acceptance:** The marine prototype shall complete repeatable recharge using the defined marine charge interface.

---

### 15. Expeditionary and Defense-Support Variant Requirements
#### EXP-001
**Requirement:** The expeditionary variant shall maintain safe operation in the absence of external network connectivity.

**Verification:** D, T

**Acceptance:** Network-isolated operation shall preserve all core safety and local-operability functions.

#### EXP-002
**Requirement:** The expeditionary variant shall support rapid module swap or service isolation using field-practical access methods.

**Verification:** D

**Acceptance:** A trained technician shall complete the defined swap or isolation task within the service-time target set by the design baseline.

#### EXP-003
**Requirement:** The expeditionary variant shall tolerate defined input-source disturbances through regulated interface design and protective control.

**Verification:** T

**Acceptance:** External-source disturbance testing shall show no unsafe state transition or uncontrolled output collapse.

#### EXP-004
**Requirement:** The expeditionary variant shall preserve control and communications loads ahead of auxiliary loads during degraded operation.

**Verification:** T

**Acceptance:** Degraded-mode testing shall show correct priority retention and load shedding.

#### EXP-005
**Requirement:** The expeditionary variant shall retain fault history suitable for offline after-action maintenance analysis.

**Verification:** D, T

**Acceptance:** Post-event logs shall remain retrievable after source interruption and controlled restart.

#### EXP-006
**Requirement:** The expeditionary variant shall support service labeling and access patterns usable under poor lighting and while wearing protective gloves.

**Verification:** D, I

**Acceptance:** Human-factors inspection and service demonstration shall show acceptable use under the defined service conditions.

---

### 16. Verification Requirements
#### VER-001
**Requirement:** Every requirement in this document shall be mapped to at least one verification method.

**Verification:** I

**Acceptance:** The verification matrix shall show complete requirement coverage.

#### VER-002
**Requirement:** The program shall establish a verification matrix linking requirement ID, verification method, test procedure, and result status.

**Verification:** I

**Acceptance:** A formal verification matrix shall exist before qualification testing begins.

#### VER-003
**Requirement:** Prototype acceptance shall require closure of all safety-critical verification items.

**Verification:** I

**Acceptance:** No prototype shall be released for field evaluation with open safety-critical verification failures.

#### VER-004
**Requirement:** Environmental, electrical, and operational testing shall be executed against variant-specific mission assumptions rather than generic conditions alone.

**Verification:** I, A

**Acceptance:** Test plans shall show traceability to the actual mission profile and environment of each variant.

#### VER-005
**Requirement:** Any requirement not yet verified shall be explicitly marked as open in the verification matrix.

**Verification:** I

**Acceptance:** Verification status tracking shall contain no ambiguous or undocumented gaps.

---

### 17. Acceptance Gate for Engineering Prototype
The engineering prototype shall be considered ready for controlled field evaluation only when all of the following are true:
- all SAF requirements are verified or formally waived with engineering justification
- all SYS, ELE, CHG, THM, and CTL requirements required for the target variant are verified
- variant-specific critical load-priority behavior is demonstrated
- fault logging and retrieval are operational
- service isolation and safe restart behavior are demonstrated
- the verification matrix is current and signed by the responsible engineering lead

---

### 18. Immediate Next Artifacts
The following documents shall be generated next to make this SRS useful:
1. verification matrix
2. mission energy budget workbook per variant
3. transient load capture report
4. functional block diagram with named interfaces
5. fault table and recovery matrix
6. prototype test procedures
7. preliminary BOM and sourcing matrix
8. enclosure packaging and service-access drawing set

---

### 19. Final Statement
This SRS defines the minimum disciplined shape of the EverSource Mission Power Module program. If a design claim cannot be traced to a requirement, verified by test, and defended in review, it does not belong in the product.

---

### 20. Annex A: Verification Matrix Template
This annex defines the minimum structure for verification management. The verification matrix shall be maintained as a controlled engineering artifact and updated throughout prototype, validation, and qualification phases.

## 20.1 Verification Status Definitions
- **OPEN**: requirement not yet verified
- **PLANNED**: verification method assigned, procedure not yet executed
- **IN WORK**: verification underway
- **PASS**: verification complete and accepted
- **FAIL**: verification complete and not accepted
- **WAIVED**: requirement disposition accepted by responsible authority with written rationale
- **N/A**: not applicable to the selected variant

## 20.2 Verification Matrix Fields
Each verification record shall include at minimum:
- requirement ID
- requirement title or short description
- variant applicability
- criticality
- verification method
- verification artifact ID
- test or analysis owner
- planned phase
- status
- acceptance reference
- evidence reference
- notes or open actions

## 20.3 Verification Matrix Template
| Requirement ID | Short Description | Variants | Criticality | Method | Artifact / Procedure ID | Owner | Phase | Status | Acceptance Reference | Evidence | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|
| SYS-001 | 48 V class architecture | A/B/C/D | High | I, T | VER-PROC-001 | Systems | Phase 1 | OPEN | SRS SYS-001 | TBD | Confirm bus tolerance band |
| SYS-006 | No cloud dependency for core safety | A/B/C/D | High | I, D | VER-PROC-002 | Firmware | Phase 1 | OPEN | SRS SYS-006 | TBD | Validate isolated operation |
| ELE-007 | Controlled precharge | A/B/C/D | High | I, T | VER-PROC-003 | Electrical | Phase 1 | OPEN | SRS ELE-007 | TBD | Measure inrush profile |
| CHG-004 | Charge inhibit outside temperature range | A/B/C/D | Critical | T | VER-PROC-004 | Electrical | Phase 1 | OPEN | SRS CHG-004 | TBD | Cold and hot threshold validation |
| THM-004 | Cold preheat mode | A/C/D | High | D, T | VER-PROC-005 | Systems | Phase 1 | OPEN | SRS THM-004 | TBD | Required for cold deployment |
| SAF-003 | Main-path overcurrent protection | A/B/C/D | Critical | T | VER-PROC-006 | Electrical | Phase 1 | OPEN | SRS SAF-003 | TBD | Confirm protective action |
| SAF-007 | Safe isolation on hazardous fault | A/B/C/D | Critical | T, D | VER-PROC-007 | Systems | Phase 1 | OPEN | SRS SAF-007 | TBD | Include restart conditions |
| UMS-001 | Rail stability during transients | A | High | T | VER-PROC-008 | Electrical | Phase 2 | OPEN | SRS UMS-001 | TBD | Test with representative actuator load |
| SOV-001 | Short ride-through support | B | High | T | VER-PROC-009 | Systems | Phase 3 | OPEN | SRS SOV-001 | TBD | Define ride-through target |
| MAR-004 | Preserve navigation/comms loads | C | Critical | T | VER-PROC-010 | Systems | Phase 3 | OPEN | SRS MAR-004 | TBD | Load-shed priority validation |
| EXP-003 | Tolerate external-source disturbances | D | High | T | VER-PROC-011 | Electrical | Phase 3 | OPEN | SRS EXP-003 | TBD | Input disturbance envelope required |
| VER-003 | Safety-critical verification closure before fielding | A/B/C/D | Critical | I | VER-PROC-012 | Program | Phase 4 | OPEN | SRS VER-003 | TBD | Gate review item |

## 20.4 Verification Matrix Use Rules
1. every requirement in this SRS shall appear once and only once in the master verification matrix
2. requirements using multiple methods may reference one primary row plus linked sub-artifacts, or separate rows if traceability demands it
3. all Critical requirements shall be reviewed at every design gate
4. no field prototype shall be released with unresolved Critical failures unless formally waived with authority, rationale, risk, and mitigation
5. any change to requirement wording shall trigger a matrix review for affected verification artifacts

## 20.5 Criticality Definitions
- **Critical**: failure creates safety, mission-loss, or major protective-function risk
- **High**: failure materially degrades mission performance, maintainability, or environmental survivability
- **Medium**: failure degrades convenience, diagnostics, or secondary performance
- **Low**: failure has limited operational effect and no safety impact

---

### 21. Annex B: Mission Energy Budget Workbook
This annex defines the workbook structure required to size the battery, supercapacitor stage, charge path, and thermal system. The workbook shall be completed separately for each variant and each mission class.

## 21.1 Workbook Objectives
The mission energy budget shall:
- quantify average and peak power demand
- define duty cycle and mission duration
- quantify energy reserve requirements
- define recharge assumptions
- bound supercapacitor burst requirements
- support sizing of battery energy, current limits, and thermal strategy

## 21.2 Workbook Tabs
The workbook should contain at minimum the following tabs:
1. assumptions and constants
2. load inventory
3. mission profile
4. energy budget summary
5. burst and transient profile
6. charge and recovery model
7. thermal assumptions
8. reserve and derating model
9. variant comparison
10. revision log

## 21.3 Tab 1: Assumptions and Constants
Required entries:
- nominal bus voltage
- minimum bus voltage
- maximum bus voltage
- battery usable depth-of-discharge target
- battery round-trip efficiency assumption
- converter efficiency assumptions by rail
- temperature derating assumptions
- reserve policy percentage
- aging margin percentage
- mission duration target

### Example structure
| Parameter | Symbol | Value | Units | Source | Notes |
|---|---|---|---|---|---|
| Nominal bus voltage | V_bus_nom | 51.2 | V | Design baseline | 16S LiFePO4 nominal |
| Usable depth of discharge | DoD_use | TBD | % | Engineering policy | Conservative value preferred |
| Battery efficiency | eta_batt | TBD | % | Test or estimate | Use measured value when available |
| Reserve margin | M_res | TBD | % | Mission policy | Must reflect return or shutdown reserve |
| Aging margin | M_age | TBD | % | Reliability policy | Capacity fade allowance |

## 21.4 Tab 2: Load Inventory
List every electrical load by mission relevance.

Required columns:
- load ID
- subsystem
- load class
- rail voltage
- steady power
- peak power
- startup surge
- duty factor
- always-on flag
- notes

### Template
| Load ID | Subsystem | Load Class | Rail | Steady Power (W) | Peak Power (W) | Startup Surge (W) | Duty Factor | Always On | Notes |
|---|---|---|---|---:|---:|---:|---:|---|---|
| L-001 | Main compute | Control and compute | 24 V | TBD | TBD | TBD | TBD | Yes | Define processor mode states |
| L-002 | Comms radio | Communications | 24 V | TBD | TBD | TBD | TBD | Variant dependent | Include TX burst duty |
| L-003 | Propulsion controller | Propulsion | 48 V | TBD | TBD | TBD | TBD | No | Use measured drive cycles |
| L-004 | Navigation sensors | Safety-critical | 12 V | TBD | TBD | TBD | TBD | Yes | Include cold-start profile |
| L-005 | Auxiliary payload | Auxiliary | Variant dependent | TBD | TBD | TBD | TBD | No | Payload-dependent |

## 21.5 Tab 3: Mission Profile
Break the mission into discrete phases.

Required columns:
- phase ID
- phase name
- duration
- active loads
- ambient temperature band
- source availability
- mobility state
- recharge availability
- notes

### Template
| Phase ID | Phase Name | Duration (min) | Active Loads | Ambient Band | Source Available | Mobility State | Recharge Available | Notes |
|---|---|---:|---|---|---|---|---|---|
| P-001 | Cold standby | TBD | Compute, comms, sensors | TBD | No | Static | No | Capture heater effects |
| P-002 | Transit | TBD | Propulsion, compute, comms | TBD | Optional | Mobile | No | Use measured drive data |
| P-003 | Task execution | TBD | Payload, compute, sensors | TBD | Optional | Mixed | No | Mission-specific |
| P-004 | Return / reserve | TBD | Navigation, propulsion, comms | TBD | Optional | Mobile | No | Apply reserve rule |
| P-005 | Docked recovery | TBD | Charge system, support loads | Controlled | Yes | Static | Yes | Include charging overhead |

## 21.6 Tab 4: Energy Budget Summary
For each mission phase, compute:
- total steady power
- phase energy
- cumulative energy
- reserve threshold
- derated energy requirement

### Template
| Phase ID | Total Steady Power (W) | Duration (h) | Phase Energy (Wh) | Cumulative Energy (Wh) | Reserve Applied (Wh) | Derated Requirement (Wh) |
|---|---:|---:|---:|---:|---:|---:|
| P-001 | TBD | TBD | TBD | TBD | TBD | TBD |
| P-002 | TBD | TBD | TBD | TBD | TBD | TBD |
| P-003 | TBD | TBD | TBD | TBD | TBD | TBD |
| P-004 | TBD | TBD | TBD | TBD | TBD | TBD |
| Total |  |  | TBD |  | TBD | TBD |

### Required calculations
- phase energy = total steady power × duration
- required mission energy = sum of phase energy
- adjusted required energy = required mission energy ÷ efficiency factors
- final battery usable energy target = adjusted required energy × reserve margin × aging margin × temperature derating factor

## 21.7 Tab 5: Burst and Transient Profile
This tab exists to size the supercapacitor stage and define bus-protection requirements.

Required columns:
- event ID
- event description
- source load
- peak power
- event duration
- repetition rate
- acceptable bus droop
- battery assist allowed
- notes

### Template
| Event ID | Description | Source Load | Peak Power (W) | Duration (s) | Repetition Rate | Acceptable Bus Droop | Battery Assist Allowed | Notes |
|---|---|---|---:|---:|---|---|---|---|
| B-001 | Propulsion launch | Drive system | TBD | TBD | TBD | TBD | Yes | Must be measured |
| B-002 | Radio transmit burst | Comms | TBD | TBD | TBD | TBD | Yes | Important for expeditionary variant |
| B-003 | Sensor warm start | Payload | TBD | TBD | TBD | TBD | Yes | Variant dependent |
| B-004 | Emergency maneuver | Propulsion | TBD | TBD | TBD | TBD | Yes | Marine or unmanned variant |

## 21.8 Tab 6: Charge and Recovery Model
Use this tab to evaluate turnaround time and dock sizing.

Required columns:
- source type
- source power available
- conversion efficiency
- battery charge limit
- supercap recovery target
- recharge window
- energy recovered
- notes

### Template
| Source Type | Power Available (W) | Efficiency | Battery Charge Limit | Supercap Recovery Target | Recharge Window (min) | Energy Recovered (Wh) | Notes |
|---|---:|---:|---|---|---:|---:|---|
| Wired DC | TBD | TBD | TBD | Full or partial | TBD | TBD | Baseline source |
| Docked charge | TBD | TBD | TBD | Full or partial | TBD | TBD | Unattended mission turnaround |
| External regulated source | TBD | TBD | TBD | Partial | TBD | TBD | Expeditionary or fixed-install |
| Solar assist | TBD | TBD | TBD | N/A | TBD | TBD | Use only where justified |

## 21.9 Tab 7: Thermal Assumptions
Use this tab to capture conditions that materially affect available energy or charge acceptance.

Required entries:
- ambient temperature bands
- cell temperature assumptions by phase
- heating energy overhead
- charging inhibit thresholds
- derating factors by temperature band

### Template
| Condition | Ambient Range | Pack Temp Assumption | Charge Allowed | Heating Overhead (W or Wh) | Derating Factor | Notes |
|---|---|---|---|---|---|---|
| Cold soak | TBD | TBD | No until threshold | TBD | TBD | Critical for A/C/D |
| Nominal field | TBD | TBD | Yes | TBD | TBD | Baseline |
| Hot enclosure | TBD | TBD | Limited or yes | TBD | TBD | Converter thermal review |

## 21.10 Tab 8: Reserve and Derating Model
This tab shall define explicit reserve logic. Do not bury reserve assumptions inside hand-waving.

Required entries:
- return-to-home reserve or controlled-shutdown reserve
- emergency reserve
- aging reserve
- temperature reserve
- mission-abort threshold

### Template
| Reserve Type | Trigger | Reserved Energy or % | Applied To Variant | Purpose | Notes |
|---|---|---:|---|---|---|
| Return reserve | Below threshold | TBD | A/C/D | Preserve return or recovery | Mission dependent |
| Controlled shutdown reserve | Extended outage | TBD | B | Preserve orderly shutdown | Fixed compute |
| Emergency reserve | Critical event | TBD | All as needed | Preserve critical loads | Define load priority linkage |
| Aging reserve | End-of-life planning | TBD | All | Capacity fade allowance | Reliability policy |

## 21.11 Tab 9: Variant Comparison
Use this tab to compare the four variants with the same calculation structure.

### Template
| Variant | Mission Energy (Wh) | Adjusted Energy (Wh) | Peak Burst (W) | Required Cap Support | Recharge Window | Reserve Policy | Notes |
|---|---:|---:|---:|---|---|---|---|
| A Unmanned | TBD | TBD | TBD | TBD | TBD | TBD |  |
| B Sovereign AI | TBD | TBD | TBD | TBD | TBD | TBD |  |
| C Marine | TBD | TBD | TBD | TBD | TBD | TBD |  |
| D Expeditionary | TBD | TBD | TBD | TBD | TBD | TBD |  |

## 21.12 Tab 10: Revision Log
Every workbook revision shall record:
- revision ID
- author
- date
- mission basis changed
- assumptions changed
- reason for update

---

### 22. Annex C: Initial Engineering Baselines
These are starting points, not final values.

## 22.1 Common-Core Initial Baseline
- battery topology: 16S LiFePO4
- nominal bus: 48 V class
- first prototype usable-energy target: approximately 1 kWh class
- primary recharge: wired DC and dock support
- transient support: managed supercapacitor stage sized from measured waveforms
- mandatory thermal features: charge inhibit and heater provision for cold-use variants
- mandatory telemetry: pack voltage, pack current, battery temperature, supercap voltage, fault history

## 22.2 Baseline Questions That Must Be Answered Before Schematic Lock
- what is the maximum continuous load for each variant
- what is the maximum transient event and duration for each variant
- what reserve policy applies to each variant
- what recharge window is operationally acceptable
- what service-time target is required for field module replacement
- what environmental envelope governs each variant

---

### 23. Immediate Next Actions
The following work shall proceed next:
1. instantiate the master verification matrix for every requirement in this SRS
2. create one mission energy workbook per variant
3. capture measured load data for propulsion, compute, communications, and thermal overhead
4. define reserve policy per variant
5. convert the highest-risk OPEN verification items into formal test procedures

These five steps turn the SRS from a static document into a working engineering program.

