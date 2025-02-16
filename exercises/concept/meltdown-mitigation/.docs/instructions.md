# Instructions

In this exercise, we'll develop a simple control system for a nuclear reactor.

For a reactor to produce the power it must be in a state of _criticality_.
If the reactor is in a state less than criticality, it can become damaged.
If the reactor state goes beyond criticality, it can overload and result in a meltdown.
We want to mitigate the chances of meltdown and correctly manage reactor state.

The following three tasks are all related to writing code for maintaining ideal reactor state.

## 1. Check for criticality

The first thing a control system has to do is check if the reactor is balanced in criticality.
A reactor is said to be critical if it satisfies the following conditions:

- The temperature is less than 800.
- The number of neutrons emitted per second is greater than 500.
- The product of temperature and neutrons emitted per second is less than 500000.

Implement the function `is_criticality_balanced()` that takes `temperature` and `neutrons_emitted` as parameters, and returns `True` if the criticality conditions are met, `False` if not.

```python
>>> is_criticality_balanced(750, 600)
True
```

## 2. Determine the Power output range

Once the reactor has started producing power its efficiency needs to be determined.
Efficiency can be grouped into 4 bands:

1. green -> 80-100% efficiency
2. orange -> 60-79% efficiency
3. red -> 30-59% efficiency
4. black -> <30% efficient

These percentage ranges are calculated as `(generated_power/theoretical_max_power)*100`
where `generated_power = voltage * current`

Implement the function `reactor_efficiency()`, with three parameters: `voltage`,
`current`, and `theoretical_max_power`.
This function should return the efficiency band of the reactor : 'green', 'orange', 'red', or 'black'.

```python
>>> reactor_efficiency(200,50,15000)
'orange'
```

## 3. Fail Safe Mechanism

Your final task involves creating a fail-safe mechanism to avoid overload and meltdown.
This mechanism will determine if the reactor is below, at, or above the ideal criticality threshold.
Criticality can then be increased, decreased, or stopped by inserting (or removing) control rods into the reactor.

Implement the function called `fail_safe()`, which takes 3 parameters: `temperature`,
`neutrons_produced_per_second`, and `threshold`, and outputs a status code for the reactor.

- If `temperature * neutrons_produced_per_second` < 40% of `threshold`, output a status code of 'LOW'
  indicating that control rods must be removed to produce power.

- If `temperature * neutrons_produced_per_second` are within plus or minus 10% of the `threshold`
  the reactor is in _criticality_ and the status code of 'NORMAL' should be output, indicating that the
  reactor is in optimum condition and control rods are in an idea position.

- If `temperature * neutrons_produced_per_second` is not in the above-stated ranges, the reactor is
  going into meltdown and a status code of 'DANGER' must be passed to immediately shut down the reactor.

```python
>>> fail_safe(temperature=1000, neutrons_produced_per_second=30, threshold=5000)
'DANGER'
```
