### 4.5.2 Motion: Automatic Path Generation

This function automatically generates and moves along a specific pattern trajectory on a designated plane while maintaining the force control state.

[F2: System] ➔ [4: Application Parameter] ➔ [24: Force Control] ➔ [3: Force Control Options] ➔ **Select [Motion] Tab**

---

![](../_assets/_15_fctrl_motion_type.png)

##### **[Motion Type]**

Provides a total of three trajectory generation modes depending on the purpose of use.

* **Spiral (Spiral Motion):** Generates a trajectory that expands outward in circles from a center point. (e.g., Grinding, Polishing processes)
* **Bidir (Bidirectional Motion):** Generates a reciprocating trajectory to fill a surface. (e.g., Surface machining of large areas)
* **Unidir (Unidirectional Motion):** Generates a trajectory that repeatedly runs in one direction and returns. (e.g., Sanding, Dispensing processes)

---

###### **1. Spiral (Spiral Motion)**

This function generates a path that starts from a center point and expands its radius in a concentric circular form.

| Item Name | Description |
| :--- | :--- |
| **Speed** | The TCP linear velocity moving along the spiral trajectory (Unit: mm/sec) |
| **Radius** | The maximum radius of the spiral to be expanded finally (Unit: mm) |
| **No. of Revolutions** | The total number of rotations from the start point to the end point (Unit: rev) |

---

###### **2. Bidir (Bidirectional Motion)**

This function generates a continuous linear path in a reciprocating form while changing the direction of the end-effector machining.

![](../_assets/_16_fctrl_ctrl_motion_bidirectional.png)

| Item Name | Description |
| :--- | :--- |
| **Speed** | The TCP linear velocity moving along the path (Unit: mm/sec) |
| **Travel Direction** | The main machining operation direction (+X, -X, +Y, -Y) |
| **Travel Length** | The single-run scale distance of the main machining path (Unit: mm) |
| **Line Break Direction** | The pitch movement direction skipping to the next line (+X, -X, +Y, -Y) |
| **Line Break Length** | The pitch distance between adjacent lines (Unit: mm) |
| **Corner Radius** | The rounding radius of the corner section where the line changes direction (Unit: mm) |

{% hint style="info" %}

**Corner Radius Configuration Limit:** The maximum value of the corner radius cannot exceed half of the smaller value between the [Travel Length] and the [Line Break Length].

{% endhint %}

---

###### **3. Unidir (Unidirectional Motion)**

To always maintain a constant forward operation, this function generates a path that shifts to the next line by returning to the starting axis after a one-way travel.

![](../_assets/_17_fctrl_ctrl_motion_unidirectional.png)

| Item Name | Description |
| :--- | :--- |
| **Speed** | The TCP linear velocity moving along the path (Unit: mm/sec) |
| **Travel Direction** | The unidirectional machining operation direction (+X, -X, +Y, -Y) |
| **Travel Length** | The distance of a single one-way machining path (Unit: mm) |
| **Line Break Direction** | The pitch movement direction skipping to the next line (+X, -X, +Y, -Y) |
| **Line Break Length** | The pitch distance between adjacent lines (Unit: mm) |
| **No. of Lines** | The total number of lines to be generated according to the designated travel direction and line break length (Unit: ea) |

---

{% hint style="info" %}

**Coordinate System Guide:** All automatic path generation functions (Spiral, Bidir, Unidir) calculate 2D trajectories based on the **XY plane of the reference coordinate system** specified in the force control coordinate system configuration item.

{% endhint %}