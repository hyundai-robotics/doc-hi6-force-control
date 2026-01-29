# 3. Force Control Commands

This section provides an overview of the main commands related to the force control feature.  
Each command is used to configure force settings, start/stop control, and execute motions like spiral, bidirectional anc zig-zag movement.

<br>

---

### List of Force Control Commands

| Command               | Description                              | Argument                | Note                     |
|------------------------|------------------------------------------|--------------------------|--------------------------|
| `fctrl on, cnd=`       | Start force control with given condition | `cnd=condition number`   | Required to start control |
| `fctrl control, cnd=`  | Change control condition only            | `cnd=condition number`   | Changes only control set during operation |
| `fctrl off`            | Stop force control                       | None                     | -                        |
| `fctrl motion_on`      | Start raster motion                      | None                     | Uses preset raster motion |
| `fctrl motion_off`     | Stop raster motion                       | None                     | Stops immediately        |
| `motion_state()`         | Check raster motion status               | None                     | -                        |
| `contact_state()`         | Check contact status               | None                     | -                        |
| `cfo(crd, type)` | Retrieves current FT sensor data | `crd`: coordinate frame defined in cnd<br>`type`: must be `"sensor"` | If the coordinate frame does not match the one configured in cnd, values will not update. The type parameter must be `"sensor"` to acquire FT sensor data. |

<br>
