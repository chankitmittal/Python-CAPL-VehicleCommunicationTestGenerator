# Automated CAPL Test Generator using Python 🚗⚡

An automation framework written in Python to parse Controller Area Network database files (`.dbc`, `.arxml`) and automatically generate comprehensive CAPL (`.can`) and test inclusion (`.cin`) modules for automated Hardware-in-the-Loop (HIL) and sil validation setups using Vector CANoe.

## 🌟 Key Features & Test Coverage

The tool automates the tedious, repetitive code creation process required for ECU validation suites by auto-generating the following edge-case testing structures:

* **Signal Range Validation:** Automates loops to sweep target signals across their entire boundary profile (`Min` to `Max`) derived strictly from the DBC factor, offset, and bit length configurations.
* **Invalid Signal Injection & DTC Verification:** Injects corrupt, out-of-bounds raw metrics (e.g., forcing a value of `0xFF` on bounded profiles) while concurrently calling UDS diagnostics (`ReadDTCInformation`) to assert proper confirmation of target DTCs.
* **Timeout & Global Node Loss:** Drops cyclic message transmissions or entire cluster nodes to verify network health fallback mechanics, timeout timers, and network management flags.
* **E2E Protection (CRC & SQC Faults):** Purposefully corrupts cyclic End-to-End profiles by calculating invalid Checksums (CRC) or skipping Alive/Sequence Counters (SQC) for a user-specified loop duration to test receiver defensiveness.
* **DLC Mismatch Verification:** Transmits frames with incorrect Data Length Codes (DLC) to ensure targeted ECUs drop or filter invalid message lengths.

---

## 🛠️ Quick Start

**Clone the directory in Command prompt**:
git clone "Repo-link"

## Execution

1. Run **Comms_Test_Generator.exe**
2. Load DBC/ARXML
3. Provide ECU Node name (Choose exact name from DBC)
4. Select Scenario from list
5. Press "Generate" button
6. Check generated CAPL files at "Output_CAPL" folder
7. Load CAN file into Test module of CANOE and Import *.vsysvar into System Variables
8. Run and Check the test results

## 📂 Repository Layout

```text
Python-CAPL-VehicleCommunicationTestGenerator/
├── CAPL_Template                 # Folder containing CAPL Templates
├── Output_CAPL                   # Generated CAPL using Example.dbc and ECU node as VCU
├── Example.dbc                   # Sample DBC file. Generated with AI
├── Comms_Test_Generator.exe      # Executable file
├── Fault_Database.json           # Contains DTC, debounce time, recovery time mapped with Message and Signal. For now generated via tool
├── Example_dbc_exported.json     # Temporary Generated file from DBC as intermediate step
├── RTE_Name_Export.vsysvar       # Automatic generation. Import this file for sysvar in CANOE
├── README.md
└── LICENSE
