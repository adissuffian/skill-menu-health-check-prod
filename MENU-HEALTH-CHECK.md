# Production Menu Health Check

Checked on 15 September 2026 against the production market homepages and `/menu` routes.

## Market against Status

| Market | Status | Evidence |
| --- | --- | --- |
| AU | Up | Pickup flow completed for Wadalba; menu rendered with categories and items. |
| NZ | Up | Pickup flow completed for Mount Eden; menu rendered with categories and items. |
| JP | Up | Pickup flow completed for Ebisu; menu rendered with categories and items. |
| FR | Up | Pickup flow completed for Gennevilliers using a future pickup time; menu rendered with categories and items. |
| BE | Up | `/menu` returned HTTP 200. |
| DE | Up | `/menu` returned HTTP 200. |
| NL | Up | `/menu` returned HTTP 200. |
| LU | Up | `/menu` returned HTTP 200. |
| SG | Up | `/menu` returned HTTP 200. |
| MY | Up | `/menu` returned HTTP 200. |
| TW | Up | `/menu` returned HTTP 200. |

The seven route-level checks returned HTTP 200 from their menu route and did not expose a transport-level error. Their complete interactive pickup flow was not executed in this run because the browser automation session was limited to one market at a time.