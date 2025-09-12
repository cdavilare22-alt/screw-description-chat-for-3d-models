# 3D Lab Best Practices Guide (Fusion 360 + PLA)

This guide is designed for engineers and lab members working with **Fusion 360**, **3D printed PLA parts**, **screws**, and **wiring**. It covers design guidelines, printing tips, parametric modeling, and practical hardware considerations.

---

## 1. Recommended Minimum Wall Thickness for Screws (PLA)

| Screw Size | Clearance Hole Ø (PLA, tuned printer) | Min Wall Thickness | Usage Notes |
|------------|---------------------------------------|------------------|-------------|
| M3         | 3.03 mm                               | 5 mm             | Hinges, lids, light loads |
| M4         | 4.03 mm                               | 6 mm             | Brackets, medium loads |
| M5         | 5.03 mm                               | 7 mm             | Structural supports |
| M6         | 6.03 mm                               | 8 mm             | Heavy duty joints |
| M8         | 8.03 mm                               | 10 mm            | Very heavy duty, uncommon in PLA prints |

**Notes:** Hole diameters assume a +0.03 mm clearance for PLA prints. Adjust if your printer tends to under- or over-extrude.

---

## 2. Screw & Hole Design Guidelines

- **Thread Engagement:** At least 2× screw diameter for direct PLA threads.  
- **Torque Limits:** Avoid overtightening:  
  - M3 → ≤ 0.5 Nm  
  - M4 → ≤ 1.0 Nm  
  - M5 → ≤ 2.0 Nm  
- **Orientation:** Print holes along Z-axis to prevent layer splitting.  
- **Reinforcement:** Use bosses (cylinder of extra material around holes) or ribs.  
- **Material Choice:** PLA is fine for prototypes; PETG/ABS if repeated assembly is needed.  
- **Infill & Walls:** ≥ 4 perimeters/walls and ≥ 30% infill around screw regions.  
- **Chamfers & Fillets:** Always add at hole edges to reduce cracking.  
- **Failure Modes:** Stripped threads, cracked walls, or insert pull-out.  
- **Tolerance Testing:** Print a small test block with multiple hole sizes to check fit.

---

## 3. Fusion 360 Modeling Best Practices

- **Parametric Design:**  
  - Use **User Parameters** for screw hole diameters, wall thickness, and boss height.  
  - Example: `M3_Hole = 3.03 mm`, `Wall_Thick = 5 mm`, `Boss_Height = 5 mm`.  
- **Sketch Constraints:** Fully constrain all hole positions and boss locations.  
- **Bodies & Components:** Model each functional part as a separate **component** (lid, hinge, bracket).  
- **Thread Features:** Fusion 360's **Thread tool** is optional; for PLA, direct drilled holes are usually sufficient.  
- **Bosses & Fillets:** Use fillets at boss bases and chamfers at hole edges to reduce stress.  
- **Joints:** Use **Rigid or Revolute joints** to simulate hinges, lids, or moving parts.  
- **McMaster-Carr Models:** Use real-world screw models from McMaster-Carr for reference when designing bosses and holes.  

---

## 4. Printing Guidelines

- **Layer Height:** 0.15–0.2 mm for better hole accuracy.  
- **Perimeters/Walls:** ≥ 4 near holes and bosses.  
- **Infill Patterns:** Gyroid or cubic for isotropic strength.  
- **Post-Processing:** Drill or ream holes if needed.  
- **Support Material:** Only where necessary; avoid contact with screw holes.  

---

## 5. Mechanical & Load Considerations

- **Load Classification:** Map screw size to light/medium/heavy expected loads.  
- **Stress Avoidance:** Avoid thin walls or sharp corners near load-bearing holes.  
- **Reinforcement Features:** Bosses, ribs, gussets, fillets.  

---

## 6. Wiring & Electronics Integration

- Maintain **minimum clearances** for wires and connectors.  
- Include **cable channels or clips** in the model.  
- Clearly mark **orientation and polarity** for connectors.  
- Avoid pinching wires when assembling with screws and bosses.  

---

## 7. Testing & Documentation

- Print **tolerance test blocks** to verify hole and screw fit.  
- Keep **assembly photos or logs** showing fits, torque, and wiring.  
- Maintain **versioning** of CAD models when changing hole diameters, wall thickness, or inserts.  

---

### Notes
This guide is a living document. Update it whenever:  
- Printer calibration changes hole fits.  
- New screw sizes or inserts are added.  
- Torque or material guidelines are revised.  
- New wiring or electronics considerations arise.