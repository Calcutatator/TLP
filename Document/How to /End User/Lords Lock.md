# The Lords Lock
The veLORDS protocol uses a locking mechanism to define the Lords they will receive. 

## Overview of the Locking Mechanism and Penalties

Users can lock their LORDS tokens for a period of up to 4 years. The longer they lock, the more voting power they receive.

- Users specify an amount to lock and an unlock time.
- The maximum lock duration is 4 years.
- Locks can only be extended in duration or increased in amount, not decreased.

## Voting Power

The voting power is calculated based on two main factors: the amount locked and the time remaining until unlock. The core formula is:

Voting Power = Amount Locked * (Duration Remaining / Total Lock Duration)

### Decay of voting power:

The voting power in veLORDS is represented as a linear function that decreases over time. This linear function is defined by two parameters:

- Bias: The y-intercept of the line, representing the initial voting power.
- Slope: The rate at which the voting power decreases over time.

The equation for voting power at any given time (t) is:

Voting Power = Bias - Slope * (t - t_initial)

***Slope Calculation***

The slope is calculated when a user locks their tokens:

Slope = Amount Locked / Lock Duration

This means that the voting power will decrease linearly such that it reaches zero exactly at the end of the lock period.

***Bias Calculation***

The bias is calculated as:

Bias = Slope * Remainder of lock duration

This sets the initial voting power proportional to both the amount locked and the lock duration.

In summary, the slope and bias system allows the veLORDS contract to:
- Represent voting power as a linear function decreasing over time.
- Accurately calculate voting power at any point in time without needing to store the full history of all users' voting power.

## Unlocking and Penalties

Users can withdraw their locked LORDS at any point but with ranging consequences. There are two scenarios:

### If the lock has expired:
   - Users receive their full amount back.

### If the lock is still active:
The user will incurr a penalty for removing their LORDS prior to the lock duration expiring.
- The penalty amount depends on how much time is remaining in your lock period.
- The closer you are to the beginning of your lock period, the higher the penalty. It starts at 75% if you withdraw in the first year.
- As time progresses, the penalty decreases gradually.

**The calculation for the penalty can be show as:**

Penalty= Amount Withdrawn × Penalty Ratio

- Time Remaining: Determine how much time is left until the end of the lock period.
- Penalty Ratio = (Time Remaining / Lock Duration) *  0.75

**Penalty Distribution:** The amount deducted as a penalty doesn’t disappear. Instead, it goes to a "reward pool," which is directed back into veLORDS holders.


### Summary
 veLORDS implements a time-weighted voting system that encourages long-term commitment to the protocol. The voting power is highest when tokens are just locked and decreases linearly as the unlock time approaches. This system aims to align the interests of token holders with the long-term success of the protocol.