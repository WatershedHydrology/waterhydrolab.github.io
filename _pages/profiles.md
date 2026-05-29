---
# =============================================================================
#  PEOPLE  ( /people/ )
# =============================================================================
#  This page lists every lab member with a photo, role, and bio.
#
#  HOW TO ADD A NEW MEMBER
#  -----------------------
#  1. Drop their photo in /assets/img/team/  (JPG or PNG, ~400×400 px).
#  2. Create a Markdown file /_pages/about_<firstname>.md with the bio.
#     See the existing about_*.md files as templates.
#  3. Add a new block to the `profiles:` list below, using `align: left` or
#     `align: right` to alternate the layout.
#  4. Keep the PI first; then current members; then alumni at the end.
#  5. Commit and push — the GitHub Actions workflow will rebuild the site.
#
#  TIP: the `align` field alternates left/right per entry, which produces
#  the zig-zag layout. Keep alternating.
#
#  TEAM PHOTOS: real headshots live in assets/img/team/ as <name>.jpeg.
#  Current members appear in the zig-zag list below; alumni are shown as a
#  photo grid in the page body (after the profiles list).
# =============================================================================
layout: profiles
permalink: /people/
title: people
description: Members of the Watershed Hydrology Lab — PI, postdocs, graduate students, research staff, and alumni.
nav: true
nav_order: 2

profiles:
  # ---------- Principal Investigator ----------
  - align: right
    image: team/golmar_golmohammadi.jpg
    image_circular: false
    bio: |
      **Dr. Golmar Golmohammadi**
      Assistant Professor — Watershed Hydrology and Biogeochemistry
      *Principal Investigator · 60% Research / 40% Extension*

      Dr. Golmohammadi leads the Watershed Hydrology Lab at the UF/IFAS Range
      Cattle Research and Education Center (RCREC) in Ona, Florida. Her research
      and Extension program focuses on watershed-scale management of soil and
      water resources of grazing lands in Florida, integrating hydrologic and
      groundwater modeling, climate-change impact assessment, and the evaluation
      of agricultural Best Management Practices (BMPs).

      She earned her Ph.D. in Bioresource Engineering from McGill University
      (2014), followed by a postdoctoral fellowship and research/lecturer
      appointments at the University of Guelph (2014–2021), in parallel with
      consulting work in water-resources protection at Aquafor Beech Ltd.
      (Ontario). She joined UF/IFAS as Assistant Professor in January 2022.

      **Affiliations:** UF/IFAS RCREC · Department of Soil, Water, and Ecosystem
      Sciences · Department of Agricultural and Biological Engineering · UF Water
      Institute.
    more_info: >
      <p><strong>Assistant Professor (PI)</strong></p>
      <p>RCREC · SWES · ABE · Water Institute</p>
      <p>Joined: Jan 2022</p>

  # ---------- Graduate students ----------
  - align: left
    image: team/saba_shaghaghi.jpeg
    image_circular: false
    bio: |
      **Saba Shaghaghi Khajehdehi**
      Graduate Research Assistant · Ph.D. Student
      *Joined June 2024*

      Saba's research focuses on surface- and groundwater interactions, nutrient
      transport, and water-quality management. She uses physically based
      watershed modeling (SWAT+) combined with data-driven and machine-learning
      approaches to predict water quantity and quality. Her work evaluates Best
      Management Practices (BMPs) and develops decision-support tools to rank and
      prioritize effective nutrient-reduction strategies within watersheds.
    more_info: >
      <p><strong>Ph.D. Student</strong></p>
      <p>SWAT+ · BMP evaluation · ML</p>
      <p>Joined: Jun 2024</p>

  - align: right
    image: team/gurjoban_tiwana.jpeg
    image_circular: false
    bio: |
      **Gurjoban Singh Tiwana**
      Graduate Research Assistant · M.S. Student
      *Joined January 2025*

      Gurjoban is from India and earned his bachelor's in Agricultural
      Engineering from Punjab Agricultural University, where his core work
      focused on watershed hydrology, soil dynamics, and precision agriculture.
      In his M.S. program he investigates the effects of nitrogen fertilization
      and irrigation on silage-corn yield and nitrate leaching in sandy
      Spodosols, integrating sensor-based monitoring to advance sustainable
      nutrient management and support environmentally responsible farming.
    more_info: >
      <p><strong>M.S. Student</strong></p>
      <p>Nitrogen & irrigation in sandy Spodosols</p>
      <p>Joined: Jan 2025</p>

  - align: left
    image: team/namrata_ghimire.jpeg
    image_circular: false
    bio: |
      **Namrata Ghimire**
      Biological Scientist II · Ph.D. Student
      *Joined May 2025*

      Originally from Nepal, Namrata completed her undergraduate studies at the
      Agriculture and Forestry University, Nepal, and earned her M.S. from South
      Dakota State University (Fall 2023), where her research focused on soil
      health under different cover crops and grazing integration. She joined
      UF-RCREC as a Biological Scientist II in August 2023 and began working with
      Dr. Golmohammadi in May 2025. Her PhD research applies AI and physically
      based models to water management and water-quality problems.
    more_info: >
      <p><strong>Biological Scientist II · Ph.D. Student</strong></p>
      <p>AI + physical models for water quality</p>
      <p>Joined: May 2025</p>

  - align: right
    image: team/armaanjot_singh.jpeg
    image_circular: false
    bio: |
      **Armaanjot Singh**
      Graduate Research Assistant · M.S. Student
      *Joined January 2026*

      Armaanjot is from Punjab, India, where agriculture and water resources
      shape daily life. He completed his bachelor's in Agricultural Engineering
      from Punjab Agricultural University and is now an M.S. student in the Soil,
      Water, and Ecosystem Sciences program. His research focuses on the
      sustainable management of soil and water resources.
    more_info: >
      <p><strong>M.S. Student</strong></p>
      <p>Sustainable soil & water management</p>
      <p>Joined: Jan 2026</p>

  # ---------- Research staff ----------
  - align: left
    image: team/akhil_reddy.jpeg
    image_circular: false
    bio: |
      **Akhil Reddy Gaddam**
      Research Data Scientist
      *Joined May 2025*

      A Computer Science graduate from the University of Florida, Akhil is a
      Software Developer (OPS) in the lab. He specializes in automating
      large-scale data pipelines and developing AI/ML models for soil,
      environment, and water data, while also building full-stack
      decision-support systems. He enjoys breaking ambiguous problems into
      achievable tasks and building meaningful collaborations.
    more_info: >
      <p><strong>Research Data Scientist (OPS)</strong></p>
      <p>Data pipelines · AI/ML · decision-support systems</p>
      <p>Joined: May 2025</p>

  - align: right
    image: team/bhavan_voram.jpeg
    image_circular: false
    bio: |
      **Bhavan Voram**
      Research Data Scientist
      *Joined May 2025*

      Bhavan is a UF Herbert Wertheim College of Engineering graduate (Jan 2023,
      Dec 2024). As a Data Scientist (OPS) in the Department of Soil, Water, and
      Ecosystem Sciences, his work focuses on data analysis and applied machine
      learning to support research in environmental and agricultural systems.
    more_info: >
      <p><strong>Research Data Scientist (OPS)</strong></p>
      <p>Applied ML for env. & ag. systems</p>
      <p>Joined: May 2025</p>
---

<div class="whl-callout" markdown="1">
**Interested in joining the lab?** We welcome inquiries from prospective
M.S., Ph.D., and postdoctoral researchers with backgrounds in hydrology,
soil and water sciences, agricultural engineering, environmental science,
and related fields.
</div>

<div class="whl-btn-row">
  <a class="whl-btn whl-btn-primary" href="/contact/#join-the-lab"><i class="fas fa-user-graduate"></i> Join the lab</a>
  <!--email_off--><a class="whl-btn" href="mailto:g.golmohammadi@ufl.edu?subject=Prospective%20student%20inquiry%20%E2%80%94%20Watershed%20Hydrology%20Lab"><i class="fas fa-envelope"></i> Email the PI</a><!--/email_off-->
  <a class="whl-btn" href="/projects/"><i class="fas fa-flask"></i> Research themes</a>
  <a class="whl-btn" href="/publications/"><i class="fas fa-book"></i> Publications</a>
  <a class="whl-btn whl-btn-ghost" href="/contact/"><i class="fas fa-paper-plane"></i> Contact</a>
</div>

## Lab Alumni

We gratefully acknowledge former lab members who contributed to our research program and have moved on to new positions.

<div class="whl-card-grid">
  <div class="whl-card whl-alum">
    <img class="whl-alum-photo" src="/assets/img/team/seyed_mostafa.jpeg" alt="Seyed Mostafa Biazar Seighalani" loading="lazy">
    <div class="whl-alum-name">Seyed Mostafa Biazar Seighalani</div>
    <div class="whl-alum-role">Former Ph.D. Student</div>
    <div class="whl-alum-dates">Jan 2023 – Dec 2025</div>
  </div>
  <div class="whl-card whl-alum">
    <img class="whl-alum-photo" src="/assets/img/team/rohith_reddy.jpeg" alt="Rohith Reddy Nedhunuri" loading="lazy">
    <div class="whl-alum-name">Rohith Reddy Nedhunuri</div>
    <div class="whl-alum-role">Former Research Data Scientist</div>
    <div class="whl-alum-dates">Apr 2023 – May 2025</div>
  </div>
  <div class="whl-card whl-alum">
    <img class="whl-alum-photo" src="/assets/img/team/maxwell_naah.jpeg" alt="Maxwell Naah" loading="lazy">
    <div class="whl-alum-name">Maxwell Naah</div>
    <div class="whl-alum-role">Former Research Assistant</div>
    <div class="whl-alum-dates">Aug 2023 – Oct 2024</div>
  </div>
</div>
