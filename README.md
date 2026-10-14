# pihole-blocklists

Small, hand-verified DNS blocklists. Every domain was observed in real traffic and
confirmed to have no functional dependency before being listed. No bulk-imported,
unvetted aggregator lists.

Generated from a home-LAN gap analysis: domains that were allowed (not caught by
existing blocklists) but look like trackers/telemetry.

## Lists

| List | Contents | Risk |
|---|---|---|
| `lists/trackers.txt` | Tracker / attribution / telemetry domains safe to block | None known — no app or device function depends on these |
| `lists/optional.txt` | Tracking-adjacent domains where blocking is a judgment call | Per-domain comments explain the tradeoff (feature flags, first-party analytics, IoT diagnostics) |

Plain-domain format (one domain per line, `#` comments) — not hosts-file format.

## Usage with Pi-hole v6

1. **Web UI → Lists → Add list**
   - Address: `https://raw.githubusercontent.com/khuang110/pihole-blocklists/main/lists/trackers.txt`
   - (optionally also `lists/optional.txt` after reviewing the comments)
2. **Tools → Update Gravity** (or run `pihole -g` on the host).

Or from the Pi-hole CLI, add the URL to `/etc/pihole/adlists.list` equivalents via the
web UI / API (v6 stores adlists in `gravity.db`); then update gravity.

## Compatibility

The plain-domain format also works with:

- **AdGuard Home** — add the raw URL as a custom blocklist
- **dnsmasq / other DNS filters** — any filter that accepts one-domain-per-line lists
- **uBlock Origin / browser filters** — importable as a custom hosts-style list

## Method

Each entry was observed as *allowed* DNS traffic over a two-week window, matched
against tracker/analytics heuristics, then individually researched to confirm blocking
would not break device or app functionality. Domains with any functional risk were
excluded (or moved to `optional.txt` with the caveat documented).

## License

MIT — see [LICENSE](LICENSE). Use freely; no warranty.
