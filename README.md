# 老虎斑 Tiger Stripe — 猫山王榴莲生理病管理 (offline PWA)

Rebuilt from 111 photos of Prof. Dr. Tran Van Hau's AgriTalk presentation, AGRI Malaysia 2026 (11 Sep 2026, MITEC).
40 unique slides (progressive builds collapsed to their final state), re-typeset as HTML/SVG in 中文 / English / Malay,
with the perspective-corrected original photo available behind a toggle on every slide.

After the slides comes a clearly-labelled 补充资料 section (not from the talk): details from the three published papers
(7-year-old trees, NPK = N:P₂O₅:K₂O, 10 L spray/tree), a source-publication card with DOIs, a symptom→cause→action
checker, a leaf-nutrient benchmark tool and bar charts of the trial tables.

The 行动计划 tab opens with an executive summary, then farms (each with tree count and several fruit-set batches),
a merged schedule with a done-log (tick each step; exported to .xlsx with three sheets: schedule log, farms,
quantities), WhatsApp share with preview, .ics calendar export, a spray-mix calculator
and an NPK mixer that converts the paper's 20-10-10 / 20-10-30 / 10-10-30 targets into grams of urea, DAP (or TSP)
and sulphate of potash — the straights the papers actually used. Muriate of potash is deliberately NOT offered.

Files
- index.html               single-file app (all images embedded as data URIs, ~5 MB)
- sw.js                    service worker — network-first, cache fallback; CACHE_VERSION is stamped by build.py on every build
- manifest.webmanifest     PWA manifest
- icon-192.png / icon-512.png / icon-512-maskable.png / apple-touch-icon.png

Deploy: push this folder as-is to a GitHub Pages repo (index.html at the root). Re-run build.py after any edit so the
cache version bumps and installed copies refresh on next open.

Data notes
- Every number was transcribed from the photos; the "View original photo" button on each slide shows the source.
- Chart values (fruit growth curves) were read off the graph and are approximate.
- The Suggestions slide had two overlapping text boxes in the original; the two bullets were untangled.

## 2026-09-12 additions
- Slide 33 retitled to **pulp** per Duong & Thuc 2026 (paper caption "nutrient contents in the pulp"; its separate leaf table gives Ca 1.69–2.00%); remark explains the professor's original title says "leaves".
- Salt spec from the paper (99% Ca(NO₃)₂ Norway / 99% MgSO₄ UK, hydration unstated) with Epsom-salt / granular-Ca(NO₃)₂ conversions in the plan's shopping list and spray calculator, and in the papers card.
- Fruit-set calibration hint in the plan linking to slides 23–24 (growth curve + development photos).
- Slide-38 care items are now dated, tickable **护理 / Care** rows in the schedule (root-zone Ca 0–50, foliar Ca 50→harvest in bad weather, no flushing 56–84, lime after harvest ≈95 DAFS); exported to WhatsApp / Excel / .ics. Log keys for care rows use the item id (`farm|batch|caroot` etc.).
- Spray rows state the trial's spray conditions (early morning, sunny, no rain).
- Per-batch **采收结果 / Harvest result** select appears once a batch is ≥ 80 days old; exported in the Excel 果园 sheet and WhatsApp text.
- **备份数据 / 恢复数据**: JSON backup of farms + log + settings (`{app:'tigerstripe', v:1, ...}`) and restore from file.
- Install hint bar above the footer: Android/desktop show an Install button (beforeinstallprompt); iPhone shows the Share → Add to Home Screen note; hidden when running standalone or after ✕ (`ts.installHide`).
- Language toggle shows 中文 / EN / BM; Malay text uses Belang Harimau for the disorder.
- Spray products are selectable (`planCfg.caSrc` gran|pure, `planCfg.mgSrc` epsom|pure; defaults = farm-shop products). `SPRAY_SRC` holds g/L per product (granular Ca nitrate 19% Ca → 5 g/L, pure → 4; Epsom ≈10% Mg → 4 g/L, anhydrous → 2), matched on Ca/Mg content; every spray figure (schedule rows, tank line, weighing card, shopping list, spray calc, WhatsApp, Excel) derives from `sprayGL(dafs)`.
- Plan settings (tank size, P source, Ca / Mg products) now sit in their own 你的药桶与肥料 block between the farms and the schedule; changes refresh schedule and quantities live without re-rendering the inputs. EN/BM use a Latin-first font stack so ’ renders normally on Windows.
- Root-zone calcium (slide 38) = three dated `drench` steps at 0 (ASAP, moves to today if entered late), 18 and 36 DAFS, using the slide-37 product/strength (Ca(NO₃)₂ 0.4%-equivalent via the product selector, 10 L/tree); included in weighing card, shopping list (Ca × 4 applications), spray calc, WhatsApp, Excel, .ics. Schedule is a single chronological checklist; today box removed; older/done rows fold under 更早 / 已做.
- Boron: the day-50 MgSO₄ spray row says to add boron to the same tank at the label rate (basis slide 12 treatment E, slide 39); a plan-only day-70 spray 'KNO₃ 1% + B' follows slide 39 (70–84 DAFS) with KNO₃ 1% from slide 11 (`PLAN_EXTRA`, slide 37 itself untouched). KNO₃ (13-0-46) is in the weighing card, shopping list, spray calc and Excel; boron is "apply per product label, never exceed it" on both sprays, shopping list and Excel — no concentration is given in the slides or papers (checked: Ca×Mg paper mentions boron once with no rate), so none is invented.
- Text size A−/A+ lives in the ☰ drawer (html[data-fs] −1…+2, key `ts.fs`), not on the main screen.

## Credits and acknowledgement
All data, photographs and the management protocol in this app come from **Prof. Dr. Tran Van Hau** (Can Tho University, Vietnam) — his AgriTalk presentation "Management of 'Tiger stripe' symptoms in Musang King in Vietnam" at AGRI Malaysia 2026, MITEC, 11 September 2026 — and the research he published with **Nguyen Huynh Duong** and **Le Vinh Thuc** at **Can Tho University**:
- Duong N.H. et al. (2025) Open Agriculture 10(1) — doi 10.1515/opag-2025-0422
- Duong N.H., Hau T.V., Thuc L.V. (2026) Crop Research 61(1–2) — doi 10.31830/2454-1761.2026.CR-1091
- Duong N.H., Thuc L.V. (2026) The Scientific World Journal — doi 10.1155/tswj/1153166

Data and photographs © the original authors and Can Tho University. This app is a non-commercial study aid compiled by Stanley Woo; where the transcription differs from the originals, the original slides and papers prevail.
- ☰ drawer → 分享此软件 / Share this app: QR code (embedded PNG, generated by build.py from qr.txt) for https://stanleywoosweeleong.github.io/Tigerstripe/, with copy-link and WhatsApp-send buttons.
- Pre-launch audit 2026-09-12: WhatsApp text is now a compact one-line-per-step format (≈ half the size) ending with the app link, and Send uses the Web Share API on phones (falls back to wa.me); .ics is RFC 5545-folded (75-octet lines) with escaped commas/semicolons; .xlsx styles carry a default cell style (no Excel/openpyxl warning).
