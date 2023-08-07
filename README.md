# tracing-slog

This fork adds support for forwarding key/value pairs from slog to tracing. It is currently experimental and depends on the [`valuable`](https://docs.rs/valuable/latest/valuable/index.html) crate and the `tracing_unstable` build flag.

**Limitations**
All key/value pairs are merged into a single hashmap and reported back as a single `kv` generic value. When serializing to JSON, this means that the value for the `kv` key is a JSON blob encoded as a string as opposed to a nested structure.

---

Adapters for connecting structured log records from the [`slog`](https://github.com/slog-rs/slog) crate
into the [`tracing`](https://github.com/tokio-rs/tracing) ecosystem.

Use when a library uses `slog` but your application uses `tracing`.

Heavily inspired by [tracing-log](https://github.com/tokio-rs/tracing/tree/60c60bef62972e447414a748a95b31ff9027165b/tracing-log).

Specifically, the emitted log entries include the custom fields `slog.target`, `slog.module_path`, `slog.file`, `slog.line`, and `slog.column` with corresponding values from the slog call site.

Note that the "native" `filename` and `line_number` metadata attributes will never be available (and `target` will always be `slog`). This is due to the fact that `tracing` requires static metadata constructed at the original call site. The `tracing-log` adapter does provide these due to explicit support in `tracing`.
