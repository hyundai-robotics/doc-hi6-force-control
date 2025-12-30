# 🧩 5. Errors & Troubleshooting

During force control operation with an external FT sensor,  
the user can monitor the **status and exception events** in real time via the UI.

---

## Force Control Exception Events & Corrective Actions

| Error Code | Primary Cause | Guide |
|:--:|---|---|
| E0260 | Force control disabled | Enable force control in the configuration |
| E0353 | Invalid force control tool number | Configure a valid tool number for force control |
| E1336 | Invalid user coordinate frame number | Configure or add a valid user coordinate frame |
| E0259 | FT sensor communication issue | Check sensor and cable connections |
| E0272 | Unsupported FT sensor | Contact customer support (sensor interface required) |
| E0273 | FT sensor communication issue | Check sensor and cable connections |
| E0274 | FT sensor communication issue | Check sensor and cable connections |

> In all exception cases, the system performs a **temporary Safe-Stop** operation as the highest priority.

---

## Troubleshooting Workflow

1. Check the FT sensor connection  
2. Verify the tool number and coordinate frame  
3. Confirm whether the sensor is supported  
4. Review and back up logs  

---
