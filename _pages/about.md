---
# =============================================================================
#  HOMEPAGE  ( permalink "/"  =>  https://watershedhydrologylab.com/ )
# =============================================================================
#  This is the lab's About / home page. Everything between the "---" fences
#  is YAML front matter that the al-folio theme reads. The content below
#  the closing "---" is the page body, written in Markdown.
#
#  COMMON EDITS:
#    - Update the `subtitle` line if titles or affiliations change.
#    - Update the `more_info` block when the lab moves offices.
#    - Tweak the announcements limit to show more/fewer news items.
#    - Re-write the body paragraphs to refresh the lab description.
# =============================================================================

layout: about # use the "about" layout — do not change
title: about # the navbar label
permalink: / # this page lives at the site root

# Subtitle appears in smaller text under the lab name on the homepage.
# We highlight Dr. Golmohammadi and her UF/IFAS affiliations as links.
subtitle: >
  Led by <a href="https://soils.ifas.ufl.edu/people/faculty/golmar-golmohammadi/">Dr. Golmar Golmohammadi</a>,
  Assistant Professor of Watershed Hydrology and Biogeochemistry ·
  <a href="https://rcrec-ona.ifas.ufl.edu/">UF/IFAS Range Cattle Research and Education Center</a> ·
  <a href="https://soils.ifas.ufl.edu/">Department of Soil, Water, and Ecosystem Sciences</a>

# ----- Landing hero -----
# Rendered by _layouts/about.liquid as an impactful banner at the top of the
# homepage: lab logo, name, tagline, primary buttons, and three research
# "pillars". Edit the tagline/pillars here; the layout handles the styling.
hero:
  logo: assets/img/whl_logo.png
  tagline: >
    Advancing the science of water across agricultural landscapes, rangelands,
    and watersheds — uniting physically based modeling, artificial intelligence,
    and a dense field-observation network to safeguard water quantity and
    quality under a changing climate.
  pillars:
    - title: Hydrologic &amp; Water-Quality Modeling
      text: Field-to-watershed simulation of flow, storage, and nutrient transport with SWAT+, MODFLOW, and DRAINMOD.
      href: /projects/1_hydrologic_modeling/
    - title: AI-Driven Environmental Risk Mapping
      text: Geospatial machine learning for flood, drought, and groundwater vulnerability, with explainable AI.
      href: /projects/2_ai_risk_mapping/
    - title: Data-Driven Decision Support
      text: Models, sensor networks, and stakeholder input to evaluate Best Management Practices for sustainable agriculture.
      href: /projects/3_decision_support/

# ----- Profile picture & contact card on the right side of the homepage -----
profile:
  align: right
  image: team/golmar_golmohammadi.jpg # path is relative to /assets/img/
  image_circular: false # set to true for a round crop
  # `more_info` is rendered as HTML directly under the photo. We use it for
  # the lab's mailing address, phone, and email.
  more_info: >
    <p><strong>UF/IFAS RCREC</strong></p>
    <p><a href="https://www.google.com/maps/search/?api=1&query=3401+Experiment+Station+Ona+FL+33865" target="_blank" rel="noopener">3401 Experiment Station<br>Ona, FL 33865</a></p>
    <p>Phone: <a href="tel:+18633747053">(863) 374-7053</a></p>
    <p>Email: <!--email_off--><a href="mailto:g.golmohammadi@ufl.edu">g.golmohammadi@ufl.edu</a><!--/email_off--></p>

# Show a "Selected publications" section below the bio. Papers marked
# `selected={true}` in _bibliography/papers.bib appear here.
selected_papers: true

# Render the row of social-media / academic-profile icons at the bottom.
# The icons come from _data/socials.yml.
social: true

# News strip on the homepage. Add files to _news/ to populate it.
announcements:
  enabled: true
  scrollable: true # add a vertical scrollbar after the first few items
  limit: 5 # max items to show; leave blank to show all

# Latest blog posts. We don't run a blog right now, so disabled.
latest_posts:
  enabled: false
  scrollable: true
  limit: 3
---

## About the Lab

The **Watershed Hydrology Lab** at the [University of Florida](https://www.ufl.edu/) /
IFAS [Range Cattle Research and Education Center (RCREC)](https://rcrec-ona.ifas.ufl.edu/)
investigates how water moves, is stored, and carries nutrients across
agricultural landscapes, rangelands, wetlands, and watersheds. Led by
[Dr. Golmar Golmohammadi](https://soils.ifas.ufl.edu/people/faculty/golmar-golmohammadi/),
our integrated research and Extension program develops sustainable water
management practices that conserve water and protect water quality under
changing climate and land-use conditions.

We combine physically based hydrologic and water-quality models (SWAT+,
MODFLOW, DRAINMOD), machine-learning and deep-learning approaches,
geospatial analysis with Earth-observation data, and an extensive
field-instrumentation network at RCREC and the DeLuca Preserve — working at
the intersection of **watershed science, artificial intelligence, and
agricultural sustainability**.
