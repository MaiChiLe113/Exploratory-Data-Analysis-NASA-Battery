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