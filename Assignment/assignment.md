# Clinician History

Hello Neha,

My name is Mr Nirmallya Mukherjee. I am the Founder of PointerNext VekXo. If you have a question, write to me at nirmallya.mukherjee@gmail.com.

You have 14 days from the day you receive this. Day 1 is today. Please send me a short design note by the end of day 4. Please send the finished work by the end of day 14.

## What you are building

I want you to build a small tool that helps a clinician look back at a ward.

A clinician starts a shift and has about a minute. A colleague may also ask, "How was the night?" Your tool should help them answer that. They will not write a database query. They will not learn a new tool while they are standing there.

Please build two things, both using the same database.

1. **A web page for the clinician.** Use Python, Flask, HTML, CSS, and jQuery. You may use one chart library. This is the page they open during the shift.
2. **Metabase, set up by you on that same database.** Metabase is where someone can slice the data freely: by ward, bed, patient, measurement, and time. Use it for exploring. The clinician should be able to get through a shift from your page alone.

Use PostgreSQL for the data. Docker is a fine way to run PostgreSQL and Metabase. Use Python 3.11 or newer. Please do not use React. Please do not build a machine learning model.

The page needs to do these three jobs. You choose the charts, the tables, and the words. I will ask you why a clinician would want them.

1. **One patient, over a time range the user picks.** Show how the numbers changed, not only the latest number. Show the usable readings, and also the hourly minimum, average, and maximum of those usable readings.
2. **One ward, beds side by side, one measurement at a time.** A person should see how the beds differ over the same hours.
3. **Readings that are not usable.** Some values are empty. Some are placeholders, called sentinel values: `-1`, `0`, and `999`. Some are numbers outside the ranges below. Show that these readings happened. Do not draw them as the patient's real oxygen, pulse, breathing, or temperature. Leave them out of the hourly minimum, average, and maximum.

A number inside the range can still be an important change. An oxygen saturation that falls from the high 90s into the 80s is inside the range. That is a real change. Please do not hide it.

For this exercise, a usable reading sits inside these ranges:

| Measurement | Usable range |
|---|---|
| SpO2 | 70 to 100 |
| Pulse | 30 to 200 |
| Breathing rate | 5 to 40 |
| Temperature | 35.0 to 42.0 °C |

A person should be able to go from the ward, to a patient, to a shorter time range, without typing ids again. If a chart is there to help a decision, put a table of the numbers next to it. Clinicians like to read the figure, not only look at a picture.

Please add any other charts, graphs, and tables you would want if you were the one coming on shift. For each extra one, write a few sentences: who uses it, and what they can see that they could not see before. If you cannot explain it that way, leave it out.

On every clinician page, show this line where it is easy to see: **Practice data. Not for real care.**

The patients and the readings are made up. You are not building something that decides a person is sick. Do not print a diagnosis. Do make a real change hard to miss.

## Who this is for

Picture the clinician, not the database.

They need to see who is on the ward, how the last many hours went, and which numbers are safe to read as the patient's. A real change in the patient, and a value that is empty, a sentinel, or off range, should not look the same. If the page turns an empty value into a zero on the chart, or hides an overnight fall because it only shows the latest number, the page has missed the point.

## The data I am giving you

Please read `data/FORMAT.md`. It explains the two files.

- `data/observations.jsonl` is what the medical monitors wrote.
- `data/assignments.csv` says which patient and which bed each medical monitor belongs to.

Each medical monitor in this file stays with one patient for the whole history. You do not need to handle a monitor moving from one patient to another. In VekXo that mapping is already taken care of, so treat the patient on each monitor as given.

A few rules. They matter.

- Save times in UTC. Show times in **Asia/Kolkata**. An "hour" means a clock hour there, such as 02:00 to 02:59.
- An empty value stays empty. Leave it out of averages. Never turn it into a real measurement. Do not invent a number to fill the hole.
- `-1`, `0`, and `999` are sentinel values. They are not the patient's reading. Leave them out of the minimum, the average, and the maximum.
- A number outside the ranges in the table above is off range. Treat it the same way: show it, and keep it out of the summary numbers.
- The same `device_id` and the same `sequence` mean the same reading, even if the line appears twice in the file.
- Some medical monitors never send breathing rate or temperature. That means they do not measure those. It does not mean the value is zero.

Most hours in the file are ordinary. A few places should change what a clinician looks at next. Finding those places, and deciding how to show them, is part of your work.

## How I would like you to work

Send questions to me. Please ask when a choice changes what a clinician would see or do. Questions about the people and the data help me more than questions about which library is allowed. Keep a note of every question and the answer I give you.

The day-4 note is where you show me that you understand the job, before the screens exist. Send it and wait for my reply before you build the application. If two working days pass and you have not heard from me, write down what you are assuming and carry on.

If some part of this write-up would lead to a tool a clinician would not use, say so in the design note and suggest something better. I want you to help shape the solution, not only follow a list.

You may use AI. Please keep a short log of what you asked, what you kept, and what you said no to, and why. When we talk at the end, you should be able to explain the work without reading that log out to me. If you cannot explain it, it is not finished.

Please use git from day 1. I will look at the history of your project.

## The day-4 note

Two to four pages of plain writing. A diagram is welcome. You do not need a working application yet.

Please answer these:

- Who opens this, at what moment, and what do they need in the first minute?
- When they ask how the night went, what are they hoping to find?
- How can they tell a usable reading from an empty value, a sentinel, or a number that is off range?
- How will a real change, still inside the range, stay visible?
- What does one row in your database stand for, and what can a person group or filter by?
- What belongs on the clinician page, and what belongs in Metabase?
- Which screens did you think about and leave out? Why would they waste a clinician's time?

## What to send me on day 14

A git project that another person can run. Please include:

- The design note, updated so it matches what you actually built.
- Scripts that load the files and build the database again from scratch.
- The clinician page, with the practice-data line.
- Your Metabase setup, or clear steps to restore it, plus a short guide to the questions you created.
- Screenshots of the pages. Please include the ward, one patient over time, a table of numbers, and how empty, sentinel, and off-range readings appear. Include Metabase as well.
- A README with the exact steps to start PostgreSQL, load the data, open your page, and open Metabase.
- The AI log.
- A short note, in a clinician's words, of what you found in this history and which screen shows it.

## When we talk at the end

I will ask you to do four things.

- Use the page the way a clinician would at the start of a shift.
- Pick one patient. Say, in one sentence a colleague could use, what you would want them to notice. Then show me where the page makes that easy to check.
- Explain what one row in your database means, and how empty, sentinel, and off-range values stay out of the averages.
- Explain one thing you decided not to build, including something an AI suggested that you did not keep.

Mr Nirmallya Mukherjee
Founder, PointerNext VekXo
nirmallya.mukherjee@gmail.com
