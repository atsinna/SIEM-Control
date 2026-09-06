# Inventory field definitions

This public inventory retains 17 recorded assets: two network devices and 15 clients. The clients comprise one Windows workstation, two Linux laptops, six phones, three tablets, and three streaming devices.

| Field | Meaning |
| --- | --- |
| Device alias | Generic identifier used consistently in public documentation; not the original hostname |
| Role | Recorded function; a monitoring role does not prove a monitoring service is deployed |
| OS family | Recorded operating-system family, including project-owner clarifications |
| Connection type | Recorded link type; Ethernet and Wi-Fi bands are not VLANs |
| Potential log availability | Available or Limited as recorded in the original inventory; not a tested collection result |

Five devices have potential logs recorded as available and 12 as limited. No claim is made that these logs are centrally collected.

## Normalization

- The original 5G connection label is represented as Wi-Fi 5 GHz, consistent with the original diagram's clarification.
- Wired labels are standardized to Ethernet.
- The primary workstation's informal purpose label is replaced with Primary workstation.
- The project owner confirmed that all six phones use iOS and Tablet-03 uses Android. These clarifications replace ambiguous device-type entries in the initial inventory.
- Trust labels are omitted because trust was not independently validated.
- Addresses, MAC addresses, and ownership data are omitted entirely.

The Excel workbook is newly created from the same public rows as the CSV. It does not reuse the original workbook's author metadata, saved local path, or unused columns.
