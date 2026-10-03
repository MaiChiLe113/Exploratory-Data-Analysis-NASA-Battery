# Battery domain notes

This project explores lithium-ion battery discharge capacity using voltage, current, temperature and experiment-order features. See the [README](../README.md) for files and columns; detailed interpretation is in the notebook and assessment report.

## Key terms

| Term | Meaning |
| --- | --- |
| Capacity | Charge delivered during a specified discharge test, measured in Ah. |
| Capacity fade | Reduction in capacity relative to a reference value. |
| State of charge (SOC) | Charge remaining relative to the battery's current full-charge capacity. |
| State of health (SOH) | Battery condition relative to a reference; capacity-based SOH is `current capacity / reference capacity × 100%`. |
| End of discharge / end of life | End of one discharge operation / a chosen health threshold for retirement. |
| Remaining useful life (RUL) | Time or cycles until end of life under assumed future usage. |
| Impedance / EIS | Electrical response to an alternating signal; impedance spectroscopy helps characterize internal battery behavior. |

## Dataset context

The data include charge, discharge and impedance tests with different temperatures, loads and voltage cutoffs. Consult the [original experiment notes](../dataset/extra_infos/) for each battery group's protocol and stopping criteria.

The current target is `Capacity`; SOC, SOH and RUL are not output labels. Capacity reflects both ageing and operating conditions, and its tertile classes are descriptive. Repeated observations require battery-aware validation, while forecasts require features available before the prediction time.

## References

- **Bole, Kulkarni and Daigle (2014).** [Adaptation of an Electrochemistry-based Li-Ion Battery Model to Account for Deterioration Observed Under Randomized Use](BatteryDamageEst.pdf). Uses an unscented Kalman filter to update battery states and ageing-related parameters from current and voltage.
- **Richardson, Osborne and Howey (2018).** [Battery health prediction under generalized conditions using a Gaussian process transition model](paper.pdf). Predicts capacity changes with uncertainty using fixed-size summaries of variable-length operating records.

These papers study randomized usage and provide background for feature preparation and battery-health analysis. The notebook does not reproduce their models or establish that their experimental datasets match the included CSVs.
