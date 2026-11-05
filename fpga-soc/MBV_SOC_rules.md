# MBV SoC Web / C / RTL Addendum
Applies together with [YJWS](../web/YJWS_v1.0.md).

- Use Part 1 Chapter 7 as the editorial reference without overwriting verified technical content.
- Keep Part 1 Chapter 11 known-good project untouched; work in separately named project copies.
- Part 2 Chapter 1 contract: UART receives a complete line on Enter; commands are exactly `LED ON`, `LED OFF`, `STATUS`. Do not silently replace with one-byte commands.
- Explain full C sources, `u8`, `u32`, AMD/Xilinx API, pointers, string parsing and memory-mapped register writes.
- Explain full RTL sources, actual ports, FSM transitions, AXI handshakes, interrupts, reset/clock, testbench and timing.
- Top is a wiring-only shell/wrapper; functional logic belongs in reusable controllers.
- Diagrams must match code identifiers and real branches. Prefer Mermaid `flowchart LR` for editable sources, SVG for published pages. Verify render and no collisions.
- Cross-check command strings, register maps, LED mapping, code, prose, tests and downloadable source links.
- Label host compilation, RTL simulation, Vivado synthesis and physical board execution separately. UVM must not be claimed unless actually run.
- Do not claim hardware success without evidence. Preserve existing working functionality and make only necessary fixes.
- Published captures and files require privacy inspection; unverified or error screenshots must not be presented as final success.
