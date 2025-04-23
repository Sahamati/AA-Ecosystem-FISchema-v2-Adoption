# FAQ – Version2 Schema Adoption

## About version2 of FI Schema

**1. What is v2 schema adoption, and who should do it?**  
**Answer:** Schema adoption refers to the process of upgrading the data structures used for FI Types to v2 as published by ReBIT. This involves making the required changes to the FI schema formats (XML, XSD), incorporating any new or modified fields, and aligning APIs and data processing accordingly.
Who should adopt v2:
- **FIPs (Financial Information Providers):** Must migrate their data formatting and transmission logic to the new v2 schema for Deposit, Recurring Deposit, and Term Deposit FI types.
- **FIUs (Financial Information Users):** Must update their data parsing and validation logic to correctly consume v2-formatted data packets.  
Adoption must follow the timelines, test coordination, and reporting guidelines issued by ReBIT in their [circular dated January 23, 2025](https://specifications.rebit.org.in/templates/NBFC-AA_Guidelines_Adoption_Deposit_RD_TD_FI_Type_Schema_Version_2.0.0.pdf).

**2. Who published the changes to the FI Schema in v2?**  
**Answer:** The changes were published by ReBIT (Reserve Bank Information Technology Pvt. Ltd.). ReBIT is responsible for maintaining and publishing technical specifications for the Account Aggregator ecosystem.  
🔗 [ReBIT Specifications Portal](https://specifications.rebit.org.in)

**3. What are the changes made in v2 of the FI Schema for Deposit, Recurring Deposit, and Term Deposit?**  
**Answer:** v2 introduces updates to:
- Field mandatory/optional status
- Newly added and deleted fields
- Data type changes
- Updated enumerations  
You can find detailed release notes for each FI Type:
- [Deposit v2.0.0 Release Note](https://specifications.rebit.org.in/api_schema/account_aggregator/ReleaseNotes/Deposit_v2.0.0_Release_Note.txt)
- [Recurring Deposit v2.0.0 Release Note](https://specifications.rebit.org.in/api_schema/account_aggregator/ReleaseNotes/RD_v2.0.0_Release_Note.txt)
- [Term Deposit v2.0.0 Release Note](https://specifications.rebit.org.in/api_schema/account_aggregator/ReleaseNotes/TD_v2.0.0_Release_Note.txt)

**4. Is it mandatory for FIPs who are not live with Term Deposit (TD) and Recurring Deposit (RD) schema to be ready with v2 schema by the adoption deadline?**  
**Answer:** It is recommended that FIPs who have not yet gone live with the Term Deposit and Recurring Deposit FI Schemas adopt version 2.0.0 in line with ReBIT’s timelines.

**5. What is the status of FI Schema version for SEBI-regulated FIPs? Have they migrated to v2?**  
**Answer:** No, SEBI-regulated FI types are still on Version 1.0.0. There have been no updates to these schemas as part of the v2.0.0 revision. Only RBI-regulated FI types—Deposit, Recurring Deposit (RD), and Term Deposit (TD)—have been updated to Version 2.0.0 (active since January 23, 2025).
SEBI-regulated FI Types include - Equity Shares, Mutual Fund Units, ETFs, IDRs, AIFs, REITs, INVITs, Bonds, Debentures, SIPs, CIS: All remain at Version 1.0.0, active since 29 December 2022 or earlier.

**6. What is the current status of Insurance FI Schemas? Have they been updated to v2?**  
**Answer:** No, Insurance FI Schemas have not been updated to Version 2.0.0. The currently active schemas, published under Version 1.0.0 by the Insurance Regulatory and Development Authority of India (IRDAI), are:
- General Insurance – v1.0.0, Active since 26 October 2023
- Life Insurance – v1.0.0, Active since 26 October 2023
However, industry adoption of even these Version 1.0.0 schemas remains very limited. Many insurers are yet to integrate or share data using these schemas.
Earlier draft schemas like Insurance Policies and ULIP were withdrawn on 08 November 2019 and should no longer be used.
Insurers are strongly encouraged to migrate to the active v1.0.0 schemas for General and Life Insurance to ensure standardization and interoperability within the AA ecosystem.

## Adoption of version 2.0.0 of FI Schema

**7. What is the adoption deadline for FIPs to migrate to Version 2.0.0?**  
**Answer:**  FIPs are expected to be 
- Production Ready by: **June 27, 2025**  
- Go-Live Window: **June 27 – July 12, 2025**  
- Decommissioning of v1.x.x: **Before July 12, 2025**

**8. What is the adoption timeline for FIUs to support and migrate to Version 2.0.0?**  
**Answer:**  FIUs are expected to be 
- Ready to Go-Live before: **June 27, 2025**  
- Support both versions: **June 27 – July 12, 2025**  
- Decommission v1.x.x: **Before July 27, 2025**

**10. Who is required to submit adoption reports for Version 2.0.0 migration?**  
**Answer:** Both FIPs and FIUs must submit adoption progress reports to ReBIT starting February 1, 2025, and every fourth week of the month thereafter.

## Testing and Implementation of Version 2.0.0

**11. Is Sahamati certification required for Version 2.0.0 of the Deposit, Recurring Deposit, and Term Deposit FI Type Schemas?**  
**Answer:** No, the current Sahamati certification framework does not cover schema validation for Version 2.0.0. It includes API-level test scenarios for FIPs but not checks related to the structure or content of the FI Schema itself. However, FIPs are strongly encouraged to comply with the Version 2.0.0 FI Schemas published by ReBIT to ensure consistency and interoperability across the ecosystem. Sahamati will soon be releasing the certification framework for FI Schema as well.

**12. Which enum value in FIType should be used: TERM_DEPOSIT or TERM-DEPOSIT?**  
**Answer:** Use TERM_DEPOSIT. As per the v2.0.0 AA APIs Release Notes, the enum value TERM-DEPOSIT in FIType is deprecated and should not be used in the POST /Accounts/discover, POST /Accounts/link, or POST /Consent APIs.
Although TERM-DEPOSIT may still appear in ReBIT specifications for backward compatibility, it is valid only for account linkages created under v1 (APIs), and only for existing mapped consents. All new linkages and implementations after July 2024 must use the enum value TERM_DEPOSIT to comply with v2.
This is also reflected in Test ID 1002, which verifies usage of TERM_DEPOSIT in POST /Accounts/discover for v2.

**13. How can FIUs support both versions during the transition period, and how will FIPs communicate that they have migrated to Version 2.0.0?**  
**Answer:** During the **transition period**, FIUs must be capable of handling both Version 1.x.x and Version 2.0.0 of the FI Schema. FIPs will indicate which version of FI Schema they are using by indicating the same in the “version field” under “AccountHolder” in the data packet shared with the FIU. This allows FIUs to detect the schema version and process the data accordingly dynamically.

**14. If some FIPs are still using the older version, should FIUs support both versions?**  
**Answer:** Yes. Between **June 1 and July 27, 2025**, FIUs are expected to support both v1.x.x and v2.0.0 schemas.

**15. ReBIT’s adoption report includes 10 test rows — Do FIPs need to test with 10 different FIUs or AAs? What if they are not integrated with 10 AAs?**  
**Answer:** To the best of our understanding, ReBIT’s adoption guidelines require FIPs to test version 2.0.0 with 10 different FIUs, and these tests must be facilitated through Account Aggregators (AAs). If a FIP is not integrated with 10 AAs, we believe that it is in the FIPs interest to fulfill this requirement by coordinating across a mix of available AAs and FIUs to complete the 10 test scenarios.
