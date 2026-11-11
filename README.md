# Solar Sizing Calculator

A free, single-page web tool that helps homeowners and shop owners in Nigeria estimate the solar system they need. The user lists their appliances and gets a suggested inverter, panel count, charge controller and battery bank, plus a rough Naira price range, then can send the result straight to a WhatsApp number for an exact quote.

**Live demo:** https://github.com/Phantomalp/solar-sizing-calculator.

## Why I built it

Many people in Nigeria want solar but do not know what size to buy, so they overspend or buy a system that cannot carry their load. This tool gives a fast, sensible starting point before a site visit and supplier quote.

## Features

- Add any appliance from a common list, or type your own (name, watts, quantity, hours per day)
- Edit or remove any appliance; nothing is preset
- Choose how much the battery should carry and how much runs at the same time
- Shows both lithium and tubular battery options side by side with rough Naira ranges
- "Send to WhatsApp" button that prefills the full load list and the suggested system
- Works on phones, supports light and dark mode, needs no login and stores no data

## How the sizing works

All formulas run in the browser (`index.html`, plain HTML, CSS and JavaScript, no framework or backend).

1. **Daily energy (Wh)** = sum of watts × quantity × hours per day.
2. **Running load** = sum of watts × quantity, scaled by how much runs at once.
3. **Inverter** = running load ÷ 0.8 power factor × 1.2 safety margin, also checked against motor start-up demand (about twice the largest motor load added to the running load). The result is rounded up to a standard size (1, 1.5, 2.5, 3.5, 5, 7.5, 10, 15 kVA).
4. **System voltage** = 12 V up to 1.5 kVA, 24 V up to 3.5 kVA, 48 V above that.
5. **Panels** = daily energy ÷ (4.5 peak sun hours × 0.75 system efficiency), rounded up to 550 W panels.
6. **Charge controller** = array watts ÷ system voltage × 1.25, rounded up to a standard MPPT rating.
7. **Battery** = daily energy × share the battery carries, divided by usable depth of discharge and efficiency (lithium 90% and 95%, tubular 50% and 85%).
8. **Price range** = equipment estimate plus 15% for cables, mounting and breakers, shown as a range.

## Update the prices

Prices are rough planning figures for Nigeria in 2026 and change with the Naira and brand. Edit the `P` object near the top of the script in `index.html`:

```js
const P = { panel: 130000, inv: {1:120000, ...}, li: 200000, tu: 85000, ... };
```

`panel` is the price per 550 W panel, `inv` is inverter price by kVA, and `li` and `tu` are battery prices per kWh for lithium and tubular.

## Limits

This is a planning tool, not an engineering design. Real systems depend on site shading, roof space, cable runs, brand and local conditions. Always confirm with a site visit and a supplier quote.

## Run locally

Open `index.html` in any browser. No build step or install needed.

## Author
Phæntom
