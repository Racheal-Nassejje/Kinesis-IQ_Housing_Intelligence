# Pod 4 Abstract Measure Definitions

Projects 7 and 8: Landlord Asset Management and Displacement Tactics; Renter and Buyer Stock Transition.

These definitions describe what is counted, not the column names used in the data. The mapping to column names is kept in the code and the README.

## Time windows

- Feature months: February to April 2026 (train), May to June 2026 (test features).
- Target months: June to July 2026.
- Target for a ward: the eviction rate in the calendar month after the feature month.

## Measures

| # | Measure | Definition | Unit |
|---|---------|------------|------|
| M1 | Eviction filings per ward | Number of landlord-tenant board cases filed for addresses in a ward in a calendar month | Cases per ward per month |
| M2 | Tenant complaints per ward | Number of 311 property-standards complaints about residential buildings in a ward in a month. Complaints with no ward recorded ("Unknown ward", 13 requests) are excluded and reported as a count. | Complaints per ward per month |
| M3 | Renovation permit activity per ward | Number of 2026 building permit applications filed in a ward in a month | Permits per ward per month |
| M4 | Residential addresses per ward | Count of address points in a ward, used as a stand-in for the number of homes | Addresses per ward |
| M5 | Normalised rate | Any of M1 to M3 divided by M4, multiplied by 1,000 | Per 1,000 addresses |
| M6 | Next-month eviction rate (target) | M5 for M1 in the calendar month after the feature month | Per 1,000 addresses |
| M7 | Lagged signal | M2 or M3 from one or two months earlier in the same ward | Same unit as M2 or M3 |
| M8 | Complaint-to-permit link | Correlation between M2 in one month and M3 in a later month, across wards | Correlation (-1 to 1) |
| M9 | Baseline forecast | Predicted M6 equals the ward's average of M6 over earlier months | Per 1,000 addresses |
| M10 | Last-month forecast | Predicted M6 equals the ward's M6 in the previous month | Per 1,000 addresses |
| M11 | Regression forecast | Linear model using M7 signals, trained on earlier months and tested on later months | Per 1,000 addresses |
| M12 | Forecast error | Mean absolute error (MAE): average gap between predicted and actual M6 | Per 1,000 addresses |
| M13 | Early warning flag | A ward is flagged in a month when its M2 or M3 is above the average of that ward's M2 or M3 over all earlier months | Yes or no |
| M14 | Warning hit or miss | A flag is a hit if the ward's M6 in the next month is above the average of that ward's M6 over all earlier months, before the flag month. A miss is a high M6 with no flag. | Count of hits and misses |
| M15 | Registered short-term rental operators | Number of registered operators in a ward on a single snapshot date (16 November 2026 for our file). The City document (29 February 2024) is used only to check the citywide total of 8,377 operators. | Operators per ward |

## Derived figures and limits

- Spadina-Fort York operator count is derived: City total minus the other 24 wards (8,377 minus 6,276 = 2,101). The report must say so.
- M15 is a single snapshot. It is not a monthly series and must not be treated as one.
- Address points are a stand-in for homes, so every rate must say so.

## Open decisions for the group

1. Accept M15 as a snapshot measure.
2. Accept "above the ward's own average" as the early warning threshold for M13, tested on June and July with hits and misses reported.
3. Accept address points as the denominator (M4).
   
[decided, 19 Nov 2026] LTB masking: drop tenant names, landlord names and unit numbers. Keep ward, month, order type and counts only. Agreed by the group.
