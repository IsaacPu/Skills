---
name: cad-dimension-comparison-table
description: Compare a CAD-based manual point-count table with an authoritative equipment point table in an explicitly scoped building or region, write differences into the manual-table layout, and audit row, column, mapping, and formatting coverage. Use for fire-alarm, evacuation, power-monitoring, electrical-fire, and similar takeoff reconciliation workbooks; do not use for generic financial or statistical comparisons.
---

# CAD Dimension Comparison Table Skill

Produce a comparison that a reviewer can trace cell by cell. Preserve the user's counted-table layout unless the user requests another presentation.

## Establish the comparison contract

Before comparing, determine and record:

- the authoritative source and the counted/manual source;
- the exact building, region, phase, or row block in scope;
- which worksheets/systems the user actually completed;
- the row key for each sheet, such as box number, floor, loop, or zone;
- the equipment-column mapping, including aliases, merged categories, and split categories;
- the displayed difference convention if a numeric difference is requested.

Do not infer scope only from the first character of a box number. Use building labels, section markers, contiguous row blocks, neighboring context, and user-provided evidence together. Treat scope boundaries as an auditable decision.

## Normalize without destroying meaning

Normalize keys and headers for matching while retaining the original text for output and evidence.

- Normalize whitespace, common Chinese/English punctuation, letter case, full-width characters, and obvious separator variants.
- Keep identifiers as text. Do not coerce box numbers or floor labels into numbers.
- Do not remove qualifiers that distinguish equipment types, direction, size, installation method, or model.
- Maintain explicit alias mappings for confirmed equivalent labels.
- If one source splits a row or column and the other combines it, aggregate only after confirming semantic equivalence. Record the aggregation rule.
- Detect duplicate normalized keys and do not silently use the first match. Resolve them by scope or aggregate only when justified.

## Compare in both directions

For every in-scope sheet, perform all of these checks:

1. Match rows by normalized key and columns by confirmed equipment mapping.
2. Compare every mapped row-column intersection, distinguishing blank from numeric zero when the source meaning requires it.
3. Find rows present in the counted table but absent from the authoritative table.
4. Find rows present in the authoritative table but absent from the counted table, including rows whose counts are all zero except one equipment column.
5. Find equipment columns present in either table but not mapped to the other.
6. For every unmapped column, inspect in-scope non-zero cells before classifying it as:
   - a genuine missing equipment category;
   - a label alias;
   - a key, subtotal, grouping, parameter, or non-comparable field.
7. Check merged rows, split rows, duplicate keys, blank keys, repeated floor labels, and boundary rows.

Never conclude that a sheet has no differences solely because mapped cells match. Unmapped rows and columns are separate failure modes.

## Write differences into the counted-table layout

Follow the user's formatting instructions first. Unless the user specifies otherwise:

- leave identical cells unchanged and visually neutral;
- when a nonblank counted value differs, replace the displayed content with `原值\n真实值：X` and color the complete text red;
- when the counted cell is blank but the authoritative value is non-zero, use a light-orange fill and red text `真实值：X`;
- when the authoritative source has a whole row missing from the counted table, reuse a reserved blank row or append a row that matches the table format, write the row key, and mark every non-zero authoritative value with the same light-orange/red treatment;
- if a genuine authoritative equipment column has no counted-table column, extend the table only when that is needed to expose an in-scope non-zero omission; copy the neighboring header/body style and label it with the authoritative equipment name;
- do not create a separate right-side comparison pane unless the user explicitly requests one.

If multiple source rows are legitimately aggregated into one output cell, the displayed original value must equal the compared aggregate, not an arbitrary component row. Add a compact note only when the aggregation would otherwise be misleading.

## Mandatory audit before delivery

Run an independent audit of the generated comparison data and the exported workbook.

### Data audit

- Recompute the comparison from the two sources, not from the formatted output.
- Reconcile counts for matched rows, unmatched rows in both directions, mapped columns, unmapped columns, and difference cells.
- Confirm every in-scope non-zero authoritative cell is either matched to a compared output cell or explicitly classified as non-comparable.
- Confirm every red or orange output cell corresponds to a real difference.
- Confirm identical values remain unmarked.
- Sample at least one ordinary mismatch, one blank-to-value mismatch, one whole-row omission, one alias match, and one merged/split aggregation when present.

### Workbook audit

- Re-import the exported workbook.
- Inspect representative key ranges and computed styles.
- Scan for formula errors and accidental helper or comparison panes.
- Render every changed worksheet and review headers, appended rows, red text, orange fills, wrapping, clipping, and row heights.
- Compare unchanged regions against the counted-table source so unrelated content and formatting remain intact.
- Open or verify the final saved path, not only an intermediate copy.

If an audit exposes a defect, update the mapping or builder, regenerate the comparison, and rerun the affected audit. Report unresolved ambiguity rather than hiding it.

## Deliverable report

Summarize:

- scope and included systems;
- difference counts by system;
- whole-row and whole-column omissions found;
- mappings or aggregation rules that required judgment;
- verification performed and any unresolved limitations.

Do not call the result complete if any in-scope non-zero authoritative cell remains unexplained.
