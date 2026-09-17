---
name: menu-health-check
description: "Check if the menu for each Domino's market is up or down in the production environment. Use when: verifying menu availability, checking market health, production menu status, market menu up/down check."
argument-hint: "Specify market codes (e.g., AU, NZ, JP) or 'all' to check every market"
---

# Menu Health Check — Production Environment

Check whether the ordering menu is accessible for each Domino's market in the production environment by navigating through the order flow.

## When to Use

- Verify menu availability across markets after a deployment
- Check if a specific market's menu is up or down in production
- Validate production environment health before release

## Market URLs

| Market | Code | Production URL |
|--------|------|-----------|
| Australia | AU | https://order.dominos.com.au/ |
| New Zealand | NZ | https://order.dominos.co.nz/ |
| Japan | JP | https://internetorder.dominos.jp/ |
| France | FR | https://commande.dominos.fr/ |
| Belgium | BE | https://order.dominos.be/ |
| Germany | DE | https://bestellen.dominos.de/ |
| Netherlands | NL | https://bestellen.dominos.nl/ |
| Luxembourg | LU | https://order.dominos.lu/ |
| Singapore | SG | https://order.dominos.com.sg/ |
| Malaysia | MY | https://order.dominos.com.my/ |
| Taiwan | TW | https://order.dominos.com.tw/ |

## Test Data

Refer to [market test data](./references/market-test-data.md) for official CI/Stage test stores and addresses for each market.
Source: [CI STAGE Test Data NextGen OLO App](https://dominos.atlassian.net/wiki/spaces/SellAndTrack/pages/1990721737/CI+STAGE+Test+Data+NextGen+OLO+App#Test-Stores)

## Procedure

For each market (or specified markets), perform the following steps using browser automation (Playwright MCP tools):

### 1. Open Homepage

- Navigate to the market's stage URL from the table above.
- Wait for the page to fully load.
- Take a snapshot to confirm the homepage is displayed.

### 2. Select Order Type

- Look for **Pick Up** or **Delivery** option on the homepage.
- Click on one of them (prefer **Pick Up** as it typically requires less input).

### 3. Enter Location

- **If Pick Up**: Enter the postcode or suburb from the test data into the search field.
- **If Delivery**: Enter the full delivery address from the test data into the address field.
- Wait for search results to appear.

### 4. Select Address from Search Results

- From the search results dropdown/list, click on the first matching address or suburb.
- Wait for the store list to load.

### 5. Select a Store

- From the **"Select a Store"** list, click the first available store.
- Wait for the order time screen to appear.

### 6. Select Order Time

- Look for the **"Now"** or **"Later"** button.
- If **"Now"** is available, click it.
- If only **"Later"** is available:
  1. Select any available **Order Date** from the dropdown.
  2. Select any available **Order Time** from the dropdown.
  3. Click the **"Schedule for Later"** button.
- Wait for navigation to the menu page.

### 7. Verify Menu Status

- Take a snapshot of the resulting page.
- **Menu is UP** if: The menu page loads with food categories and items visible.
- **Menu is DOWN** if: An error page is displayed, the page fails to load, or an error message is shown.

## Reporting

After checking all requested markets, produce a summary table:

```
| Market | Status | Notes |
|--------|--------|-------|
| AU     | UP     |       |
| NZ     | DOWN   | Error: "Service unavailable" |
| ...    | ...    | ...   |
```

Use visual status indicators in the final report:

- `🟢 Up` — the menu page loaded with food categories and items visible.
- `🔴 Down` — the menu failed to load, displayed an error, timed out, or a required flow step failed.

In the Notes column, identify the evidence level: `End-to-end` when the complete pickup flow was completed, or `Route-level` when only homepage/menu-route availability was verified. Do not report a route-level check as end-to-end validation.

## Error Handling

- If a page fails to load within 30 seconds, mark the market as **DOWN** with a timeout note.
- If any step in the flow fails (e.g., no stores available, address not found), note the specific failure point.
- Continue checking remaining markets even if one fails.
- Take a screenshot on failure for debugging context.

## Important Notes

- These are **production environment** URLs — they may require VPN or network access.
- Some markets may have different UI layouts or languages; adapt the flow accordingly.
- The browser tools will provide snapshots in accessibility-tree format — use these to identify buttons, inputs, and links.
