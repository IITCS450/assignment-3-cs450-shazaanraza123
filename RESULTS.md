# RESULTS — Lottery Scheduling

## Setup
3 child processes, tickets 1, 2, and 4. Total 7 tickets so expected shares are like 14%, 29%, 57%. Ratio 1:2:4.

## Workload
Each child just spins in a loop counting until 400 ticks go by. No I/O no sleep, just CPU. They all stay runnable the whole time so the scheduler is the only thing deciding who runs.

## Observed Results
One run at 400 ticks:

| Child | Tickets | Count   | Ratio  | Expected |
|-------|---------|---------|--------|----------|
| 0     | 1       | 41,823  | 1.00x  | 1.00x    |
| 1     | 2       | 82,914  | 1.98x  | 2.00x    |
| 2     | 4       | 164,209 | 3.93x  | 4.00x    |

Came out 14.4% / 28.6% / 57.0% — pretty close to expected.

## Variance
Every time the scheduler picks someone its a random draw. Few draws = more noise. More draws = numbers settle toward the real probabilities. Thats just law of large numbers. Run it longer and you get closer to 1:2:4. Short run like 40 ticks the ratios jump around a lot more.
