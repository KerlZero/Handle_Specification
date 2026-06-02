# WTTx BA Documentation Package

This documentation package is prepared from a Business Analyst perspective for the WTTx / Pocket NET WiFi sales-channel enhancement.

## Purpose

The objective of this initiative is to add WTTx / Pocket NET WiFi as an additional sales option within the normal home internet registration journey. The solution targets customers whose locations are not serviceable by standard home internet installation but can still use internet service through mobile network coverage.

## Files

- `01_Flow_Diagram.md` - End-to-end process flow with Mermaid sequence diagram
- `02_BRD.md` - Business Requirement Document
- `03_FRD.md` - Functional Requirement Document
- `04_User_Stories.md` - User stories
- `05_Acceptance_Criteria.md` - Acceptance criteria
- `06_Use_Cases.md` - Use cases and use case diagram
- `07_Business_Rules.md` - Business rules
- `WTTx_Flow_Diagram.png` - High-level BA flow diagram image
- `WTTx_Use_Case_Diagram.png` - Use case diagram image

## Scope Summary

Web Register must support WTTx / Pocket NET WiFi registration for locations where normal home internet cannot be provided. The registration journey should follow the normal home internet flow as closely as possible, with key differences including WTTx eligibility by Latitude/Longitude, no installation appointment requirement, additional payment methods before order submission, profile creation through downstream systems, and stock update through PayG before SAP posting.

## Flow_Diagram
<img width="1800" height="1150" alt="WTTx_Flow_Diagram" src="https://github.com/user-attachments/assets/60930b62-cb29-4a2e-acfc-ff5effad1ff7" />

## Use_Case_Diagram
<img width="1700" height="1100" alt="WTTx_Use_Case_Diagram" src="https://github.com/user-attachments/assets/861befba-606a-4fdb-9336-23fb4885cbf3" />

## End-to-End Sequence Flow
<img width="8192" height="6971" alt="Visitor Engagement" src="https://github.com/user-attachments/assets/088ad614-bb08-4e92-8553-1ed8e13a2137" />
