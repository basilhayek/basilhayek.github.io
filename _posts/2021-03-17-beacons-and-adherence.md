---
title: Beacons and Adherence
published: true
---
I recently started taking medicine to help manage my cholesterol levels. I opted for pragmatism as opposed to thinking I'd manage it via diet and exercise alone.

Twenty-four days after my first 30-day fill, I have 11 pills left. If I have perfect adherence and refill when I'm out of supply, I'll have a PDC of 86%. As adherence goes, not bad. But if I extrapolate based on my (short) history, I'll be just under that 80% adherence threshold. 

Years ago, a colleague and I had discussed using beacons to help improve adherence due to forgetfulness. Simple time-based reminders can work, but our thinking was that a contextual reminder using time and proximity to the pill bottle would be more effective. In the days before perpetual work-from-home, location could also be used to trigger an urgent alert if you were about to head out to the office without taking your medication.
<!--excerpt-->

I never pulled the trigger on buying the Eddystone beacons to develop a proof-of-concept. But given my own statin journey, I shopped around and found a multi-protocol BLE beacon with a push button for $20.

So now the task is to develop a proof-of-value adherence app that uses a BLE beacon to remind me to take my medication.

I'm planning to push the button on the beacon when I take the medication. If I haven't pushed the button within a certain time, my phone will remind me.

Seems pretty straightforward. I'm not planning on using proximity for this, as I think the approach above should offer most of what I need. 

Time to start building!
