# Yuul-Jung Web Standard (YJWS) v1.0
Status: normative core; established 2026-11-05.
Scope: learning sites, technical docs, reports, portals, dashboards, project introductions.

## 1. Separation and precedence
- CORE: semantic HTML, full-width layout, default Light theme, optional Dark theme, responsive design, accessible navigation, privacy and release checks.
- PROFILES: docs / article / dashboard / landing. Do not force a 3-column docs layout onto every site.
- COMPONENTS: code, explanation, tables, SVG diagrams, screenshots, checklists, verification panels.
- DOMAIN: source-specific requirements such as MBV SoC C/RTL, UART protocol, AXI register map and tool instructions.
- Verified source and technical contracts always outrank illustrative UI examples. Preserve valid legacy content during restyling.

## 2. Layout
- Fill the available viewport width; do not impose a narrow global max-width.
- Desktop docs: collapsible left chapter navigation, flexible central content, collapsible right in-page table of contents.
- On smaller screens, collapse sidebars without horizontal page overflow.
- Text paragraphs may use readable line lengths; code, diagrams, tables and screenshots may use the entire available central width.
- Use an 8px spacing scale and reusable tokens; avoid decorative excess.
- Validate at 1920, 1366, 1024, 768, 390 and 320 CSS pixels.

## 3. Theme
- Initial theme is ALWAYS Light unless the user explicitly saved Dark.
- Never default to operating-system dark preference.
- Visible Light/Dark toggle and Alt+T keyboard shortcut (unless a browser shortcut conflicts).
- Persist manual choice in localStorage when available; handle storage failures.
- All code, tables, SVGs and diagrams must remain readable in both themes.
- Print uses a readable Light presentation. Theme changes must not affect content semantics.

## 4. Navigation and accessibility
- Use header, nav, main, aside and footer appropriately; one meaningful H1 per page.
- Provide skip-to-content, visible keyboard focus, accessible labels and current navigation state.
- Link in-page TOC to real section IDs; ensure anchor navigation accounts for sticky headers.
- Interactive buttons must work via keyboard; never make decorative controls.
- Use descriptive links, image alt text, sufficient contrast and reduced-motion support.

## 5. Technical content
- Preserve full source code where the task calls for it; identify language, file, version and validation status.
- Use code + concise explanatory comments + directly adjacent explanation.
- Explain unfamiliar types, APIs, macros, bit operations, pointer use and I/O mappings against real code.
- Show conceptual diagrams separately from verified code-level diagrams.
- SVG is preferred for precise HTML diagrams; verify labels, edges and actual rendering. No text/line overlap.
- Keep source names, signals, states, command strings and register addresses consistent across text, tables and figures.
- Use responsive scrolling for large tables and long code without clipping.

## 6. Reliability, privacy and publishing
- Source-of-truth hierarchy: verified source code and specifications → confirmed tests → explanatory prose → illustrative examples.
- Distinguish PASS / FAIL / NOT VERIFIED / N/A. Never label a simulation-only result as hardware verified.
- Review public pages and screenshots for names, addresses, tokens, internal paths, account details and metadata.
- No third-party dependencies by default; document and justify any added dependency.
- Verify links, asset paths, print output, responsive widths, keyboard use, theme persistence and JS-disabled fallback.
- Make minimal changes to correct issues; record material changes and test evidence.
- A visually attractive result is not sufficient without technical and privacy checks.

## 7. Template contract
- Shared CSS variables, navigation components and theme logic must be reused.
- Content must be separable from layout; new chapters should not fork the design system.
- All sample commands and code in the template are explicitly illustrative until matched to source.
- The repository's web/template/index.html is a demonstrator, not proof of real board validation.

## 8. Release gate
1. Identify actual source and target audience.
2. Choose profile; render content with shared components.
3. Check source-to-text-to-diagram consistency.
4. Run responsive and accessibility checks.
5. Run privacy and security inspection.
6. Record PASS, FAIL or NOT VERIFIED per check.
7. Publish only reviewed public-safe content.

## 9. MBV SoC extension
See ../fpga-soc/MBV_SOC_rules.md. Keep UART line commands, actual C/RTL source, AXI mapping and board verification as domain contracts rather than generic web defaults.
