# gmsol_store (GMTrade / GMX-Solana) IDL — generics-stripped

`gmsol_store_stripped.json` is the gmsol-labs/gmx-solana **store program** IDL with its 25 generic
typedefs removed, so it loads with the consumer repo's `UnmarshalRawIdl`, which rejects the Anchor
`{"generic":"T"}` type shape. **Derived output — regenerate from the source, do not hand-edit.**

- **Program:** `Gmso1uvJnLbawvw7yezdfCDcPydwW2s2iqG3w6MDucLo`
- **Source:** `gmsol-labs/gmx-solana` `crates/programs/idls/gmsol_store.json`, version **0.12.0**, pin
  `61e0a6530d` (sha256 `98cad259…`, 860617 bytes).
- **Strip filter:**
  `jq '.types |= map(select([.. | objects | select(has("generic"))] | length == 0))' gmsol_store.json`
- **Result:** 139 instructions, 32 events, 156 types (25 generic typedefs dropped), 0 remaining generics.
- **Signature** (keccak256 of these served bytes, for `gmxIdlSignature` in the consumer):
  `fd882594cf376053e2f2228b8024be491ab14989f405f07187620ea5334638fe`
- **Accepted cost:** the generic-referencing events `MarketFeesUpdated`, `PositionIncreased` (and up to
  two more) lose their typedef and `event_decode_failure`; they are phase-2/3 events the perpetual
  parser does not read. See `streaming_processor_solana` `_docs/topics/gmtrade/README.md`
  ("Registration and cutoff").
