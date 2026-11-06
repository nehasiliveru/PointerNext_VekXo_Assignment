# The two data files

I made this data up for your assignment. The clinic, the people, and the readings are not real. This is not a medical record, and it is not for real care.

The history runs from **27 October 2026, 08:00** to **1 November 2026, 08:00**, India time (Asia/Kolkata). The last reading is at 07:55. The times inside the files are UTC.

## observations.jsonl

Each line is one JSON object. A medical monitor wrote each line.

```json
{"device_id":"dev-example","captured_at":"2026-10-27T02:30:00Z","parameter_code":"SPO2","value":97,"unit":"%","sequence":1}
```

```json
{"device_id":"dev-example","captured_at":"2026-10-28T08:40:00Z","parameter_code":"SPO2","value":null,"unit":"%","sequence":2}
```

These two lines only show the shape. They are not rows from the file.

| Field | Meaning |
|---|---|
| `device_id` | Id of the medical monitor. It does not change |
| `captured_at` | UTC time the reading was taken, written as `YYYY-MM-DDTHH:MM:SSZ` |
| `parameter_code` | What was measured. The list of codes is fixed |
| `value` | The number, or `null` when the value is empty |
| `unit` | The unit for that code |
| `sequence` | A counter for that medical monitor. A new reading gets the next number. A copy of the same reading keeps the same number |

The same `device_id` and the same `sequence` mean the same reading. If that pair shows up again, it is the same reading sent a second time.

The time between readings is not always the same.

| Code | Unit | In plain words |
|---|---|---|
| `SPO2` | `%` | Oxygen saturation |
| `PULSE` | `bpm` | Pulse rate |
| `RR` | `breaths/min` | Breathing rate |
| `TEMP` | `C` | Temperature |

Some medical monitors send only `SPO2` and `PULSE`. If a code never appears for a monitor, that monitor does not measure it.

`null` means the value is empty. `-1`, `0`, and `999` are sentinel values. They stand in for "no real reading". Other numbers can fall outside a usable range. Your assignment note explains which ranges to use.

## assignments.csv

This file says which patient and which bed each medical monitor belongs to. One row per monitor. The monitor stays with that patient for this whole history.

`valid_from` is the start of the history, in UTC.
