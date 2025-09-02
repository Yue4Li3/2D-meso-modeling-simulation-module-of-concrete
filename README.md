# 2D-meso-modeling-simulation-module-of-concrete
2D mesoscopic modeling tool for bridge concrete with controllable aggregate size, shape, gradation, and content.

# 2D Mesoscopic Modeling and Simulation Module for Bridge Concrete

A lightweight module for generating **2D mesoscopic concrete models** with controllable specimen size, aggregate type, gradation, and volume fraction.  
The tool is designed for **research in bridge concrete materials**, supporting both image-based and vector-based outputs.

---

## ✨ Features

### Input Parameters
- **Model boundary (specimen size):** dropdown (`100×100 mm`, `200×200 mm`, `custom`)  
- **Aggregate type:** radio button (`circular`, `elliptical`, `polygonal`)  
- **Aggregate content:** single slider (`0% – 80%`)  
- **Aggregate gradation:** dropdown (`Fuller`, `custom`)  
- **Particle size range:** double slider (`0.5 mm – 30.0 mm`)  

### Output Results
- **Concrete cross-section image** (`.jpg`)  
- **Concrete cross-section vector model** (geometry file, e.g., `.svg` or `.json`)  

---

## 📖 Short Description
This module provides a **mesoscopic modeling platform** for concrete cross-sections, based on an embedded aggregate parameter library.  
It enables parameterized generation of aggregate geometries that match real bridge concrete material characteristics.

---

## 📚 Full Description
As material modeling frameworks and simulation technologies advance, **capturing the internal geometry of concrete** has become increasingly important.  
Since aggregates determine the spatial distribution of cement paste and the interfacial transition zone (ITZ), their geometry strongly influences material performance.

Key aspects addressed in this module:  
1. **Aggregate size distribution**  
   - 3D gradation is typically based on cumulative distribution functions (CDF) of volume or mass.  
   - For 2D models, area-based CDFs are derived from 3D functions.  
   - Example: *Walraven function* converts Fuller gradation into 2D particle size distribution under the spherical aggregate assumption.  

2. **Aggregate shape generation**  
   - In 2D, shapes can be circular, elliptical, or polygonal.  
   - In 3D, shapes extend to spherical, ellipsoidal, polyhedral, or more complex particle models.  
   - Shape descriptors (aspect ratio, angularity) are introduced through probabilistic distributions.  

3. **Modeling workflow**  
   - Step 1: Monte Carlo sampling from the particle-size CDF to generate a particle diameter.  
   - Step 2: Sample aspect ratio distribution to define the particle geometry.  
   - Step 3: Add generated particles to the aggregate library until the required area fraction is reached.  
   - Step 4: Sequentially place aggregates from largest to smallest, randomizing orientation and position, while avoiding overlaps.  

This method, based on statistical laws, enables realistic representation of aggregate features and provides a refined foundation for mesoscopic concrete simulation.

---

## 🔧 Example Usage (Python snippet)

```python
from meso_model import generate_model

# Example: 200×200 mm specimen, 30% aggregates, elliptical, Fuller gradation
model = generate_model(
    size=(200, 200),
    agg_type="elliptical",
    agg_fraction=0.30,
    gradation="Fuller",
    size_range=(0.5, 30.0)
)

# Save results
model.save_image("AGin_200_30_example.jpg")
model.save_vector("AGin_200_30_example.json")
