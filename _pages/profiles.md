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
    content: about_golmar.md
    image_circular: false
    more_info: >
      <p><strong>Assistant Professor (PI)</strong></p>
      <p>RCREC · SWES · ABE · Water Institute</p>
      <p>Joined: Jan 2022</p>

  # ---------- Graduate students ----------
  - align: left
    image: team/saba_shaghaghi.jpeg
    content: about_saba.md
    image_circular: false
    more_info: >
      <p><strong>Ph.D. Student</strong></p>
      <p>SWAT+ · BMP evaluation · ML</p>
      <p>Joined: Jun 2024</p>

  - align: right
    image: team/gurjoban_tiwana.jpeg
    content: about_gurjoban.md
    image_circular: false
    more_info: >
      <p><strong>M.S. Student</strong></p>
      <p>Nitrogen & irrigation in sandy Spodosols</p>
      <p>Joined: Jan 2025</p>

  - align: left
    image: team/namrata_ghimire.jpeg
    content: about_namrata.md
    image_circular: false
    more_info: >
      <p><strong>Biological Scientist II · Ph.D. Student</strong></p>
      <p>AI + physical models for water quality</p>
      <p>Joined: May 2025</p>

  - align: right
    image: team/armaanjot_singh.jpeg
    content: about_armaanjot.md
    image_circular: false
    more_info: >
      <p><strong>M.S. Student</strong></p>
      <p>Sustainable soil & water management</p>
      <p>Joined: Jan 2026</p>

  # ---------- Research staff ----------
  - align: left
    image: team/akhil_reddy.jpeg
    content: about_akhil.md
    image_circular: false
    more_info: >
      <p><strong>Research Data Scientist (OPS)</strong></p>
      <p>Data pipelines · AI/ML · decision-support systems</p>
      <p>Joined: May 2025</p>

  - align: right
    image: team/bhavan_voram.jpeg
    content: about_bhavan.md
    image_circular: false
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
  <a class="whl-btn" href="mailto:g.golmohammadi@ufl.edu?subject=Prospective%20student%20inquiry%20%E2%80%94%20Watershed%20Hydrology%20Lab"><i class="fas fa-envelope"></i> Email the PI</a>
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
