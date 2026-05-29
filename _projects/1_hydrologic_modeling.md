---
# =============================================================================
#  Research project — Hydrologic & Water Quality Modeling
# =============================================================================
#  Each file in /_projects/ becomes a card on /projects/ and its own page.
#  `importance` controls sort order (lower = earlier). `category` becomes a
#  filter tab on the projects index.
# =============================================================================
layout: page
title: Hydrologic & Water Quality Modeling
description: Process-based modeling of flow, storage, and nutrient dynamics at field and watershed scales.
img: assets/img/research_hydrology.jpeg
importance: 1
category: research

# ----- Buttons at the foot of the page (edited in the CMS, no HTML) -----
buttons:
  - {
      label: "Collaborate on this research",
      url: "mailto:g.golmohammadi@ufl.edu?subject=Collaboration%20%E2%80%94%20Hydrologic%20%26%20Water%20Quality%20Modeling",
      icon: "fas fa-handshake",
      style: "primary",
    }
  - { label: "Meet the team", url: "/people/", icon: "fas fa-users" }
  - { label: "All publications", url: "/publications/", icon: "fas fa-book" }
  - { label: "Field instrumentation", url: "/facilities/", icon: "fas fa-microscope" }
  - { label: "All research themes", url: "/projects/", icon: "fas fa-arrow-left", style: "ghost" }
---

We develop and apply physically-based hydrologic and water-quality models
to quantify water flow, storage, and nutrient dynamics across agricultural
landscapes, rangelands, wetlands, and watersheds. Our work links field-scale
processes to watershed-scale outcomes, with particular attention to
**nutrient transport, runoff generation, and hydrologic connectivity**.

These models support:

- Evaluation of agricultural Best Management Practices (BMPs).
- Environmental risk assessment.
- Scenario-based analysis under changing climate, land use, and management.

### Tools we use

- **SWAT+** for watershed-scale simulation of flow and water quality.
- **MODFLOW** and coupled **SWAT-MODFLOW** for integrated
  surface–groundwater modeling.
- **DRAINMOD** for tile-drained agricultural systems.
- Custom Python pipelines for data harmonization, calibration, and
  uncertainty analysis.

### Representative recent publications

See the [publications page](/publications/) for the full list. Notable
related works:

- _Compilation simulation of surface water and groundwater resources using
  the SWAT-MODFLOW model for a karstic basin in Iran_ — Hydrogeology
  Journal (2023).
- _Assessment of Impacts of Climate Change on Tile Discharge and Nitrogen
  Yield Using the DRAINMOD Model_ — Hydrology (2020).
- _Designing a deep learning-based framework for the prediction of lake
  surface closed curves_ — Earth Science Informatics (2025).

{% include whl_buttons.liquid items=page.buttons %}
