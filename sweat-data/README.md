# hDrop sweat sessions

Raw hDrop exports pasted by Jason, one file per activity, named `YYYY-MM-DD-<city>.json`.
Used to build the personal sweat/sodium model behind `race.targets.sodiumMgPerHour`
and per-segment sodium guidance. Reference point: Precision sweat test (2023) measured
1,679 mg sodium per liter of sweat (lab-stimulated, upper bound).

Units in these exports: time-series sweatRate and fluidLoss are ounces (oz/hr and
cumulative oz); metadata totalSweatLoss is liters-ish (reconcile against the oz series);
totalSodium is mg; temperature is skin temp °F; weatherTemperature is °C.
