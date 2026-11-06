The one-sentence version

Build a screen a nurse or doctor can open at the start of a shift. In about a minute it should answer two questions: “Who is on my ward, and who changed?” and “Which of these numbers can I trust?” It must never let a broken sensor look like a sick patient, or a sick patient look like a broken sensor.

The moment

It is 08:00 (or 20:00). The clinician is standing at the ward, taking handover. A colleague asks, “How was the night?” They have no time to run queries, learn a tool or scroll through raw numbers. They have a minute.

What they want, in order:

Who is on the ward? Which beds, which patients, and which measurements each one has. Some monitors only send SpO2 and pulse. A missing temperature means “not measured”, not “zero”.
Did anyone change? I mean a real change: oxygen drifting down, pulse and breathing creeping up, temperature climbing. They want it even if every number stayed inside the normal range.
Was anyone’s data unreliable? Which monitor went blank, sent placeholders, or sent impossible numbers, and for how long. It matters because if the monitor was broken, nobody actually knows how the patient was doing during that time.
Then dig into one patient. Pick the person, pick the hours that matter, read the actual numbers.
The flow, step by step
 ┌─────────────────────────────────────────────────────────────┐
 │  Practice data. Not for real care.        (always visible)  │
 └─────────────────────────────────────────────────────────────┘

 STEP 1 – WARD VIEW  ("How was the night?")
   Pick ward (Medical / Observation), pick a time window (default: last shift)
   One row per bed:  Bed · Patient · what they're monitored for
        · small trend line per measurement
        · badge "Changed: SpO2 fell 97 → 88 between 01:00 and 05:00"
        · badge "Data problem: 1h 25m of unusable readings"
   Beds side by side for ONE measurement at a time (SpO2, pulse, …)
   + table of the hourly numbers next to it
          │ click a bed / patient
          ▼
 STEP 2 – PATIENT VIEW
   Time range picker (defaults to the window you came from)
   Chart: usable readings as a line, hourly min/avg/max as a band
   Table: the same hourly numbers
   Strip underneath: "Not usable" moments, shown as marks, NOT as dots on the line
          │ click an hour or drag on the chart
          ▼
 STEP 3 – NARROWER TIME RANGE
   Same patient, e.g. 02:00–06:00, every individual reading in a table,
   each tagged: Usable / Empty / Placeholder / Out of range

The context travels with the clinician. Ward, patient and time range carry through each click, and nobody types an id twice.

Telling apart the things that look similar

This is the heart of the brief. There are four different situations, and the screen must make each one look different at a glance:

What happened	What it means	How it should look
Usable reading	The patient’s real value	Normal line and dots
Empty (null)	The monitor sent nothing	A visible gap in the line. Never a zero
Placeholder (-1, 0, 999)	The monitor’s way of saying “no real reading”	A small grey marker on a separate “not usable” strip, labelled “placeholder”
Out of range (e.g. SpO2 of 120, pulse of 250)	A number the body cannot produce. The sensor is faulty	Same strip, labelled “out of range”
A real change, still in range	E.g. SpO2 97 → 88	Highlighted and hard to miss: coloured band, a “fell by 9 points” label, and the table row marked

The last row is the trap. If the page only shows the latest value, or filters “abnormal” things out, a slow overnight fall disappears. And if it plots a 0 or 999 as a real pulse, a sensor fault looks like a crisis.

The page must not print a diagnosis. It only says “this changed”, never “this patient is sick”.



I would still hold this as a first reading. The real work is deciding the thresholds for what counts as a “change” and checking each of these on screen.
