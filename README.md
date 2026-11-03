# ha-blueprints

Home Assistant blueprints, shared across multiple installations.

## Updating a blueprint

1. Edit the YAML file in this repo and push to `main`.
2. On each Home Assistant instance using the blueprint: **Settings → Automations & Scenes → Blueprints** → find the blueprint → **⋮ → Re-import blueprint**. This re-downloads from the file's `source_url` and updates the installed copy in place — existing automations built from it keep their current input values (label, threshold, etc.) unless you changed an input's name/key.
3. If you added a new input, give it a `default:` so existing automations don't break on re-import.

Only rename or remove an input's key if you're prepared to re-select inputs on every automation built from it on every instance — existing automations reference inputs by key name.

## Blueprints

### `automation/low_battery_alert.yaml` — Low Battery (by label)

Notifies when any entity carrying a chosen label drops below a battery
percentage threshold. Point it at a label (e.g. `batteri`) instead of
listing entities by hand — any device tagged with that label is covered
automatically, on any instance.

**Inputs:**
- `battery_label` (required) — the label to monitor
- `threshold_percent` (default `15`) — battery % to alert below
- `notify_action` (default: broadcast via `notify.notify`) — override to target a specific device or add critical-push flags

**Requires:** Home Assistant 2026.7.0+ (uses the `battery.level_crossed_threshold` purpose-specific trigger).
