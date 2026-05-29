---
# =============================================================================
#  CONTACT  ( /contact/ )
# =============================================================================
#  Almost everything on this page is now STRUCTURED, so it can be edited in the
#  CMS (Other Pages -> Contact) with plain fields — no HTML:
#    - "Intro callout"            : the highlighted welcome box (Markdown).
#    - "Principal Investigator"   : name, role, email, phone, address, buttons.
#    - "Map"                       : just an address (the embed is built for you).
#    - "Find us — building & ..."  : RCREC building + affiliated units (cards).
#    - "Follow the lab links"      : the social/profile buttons.
#    - "Join / Postdoc buttons"    : the call-to-action buttons.
#  Only the two prose paragraphs ("Join the Lab", "Postdoc") stay in "Page
#  content". The "email_off" markers that protect mailto links are added
#  automatically by the buttons/PI-card templates.
# =============================================================================
layout: page
permalink: /contact/
title: contact
description: How to reach the Watershed Hydrology Lab — Principal Investigator, lab address, and information for prospective students and collaborators.
nav: true
nav_order: 7

# ----- Highlighted welcome box (Markdown) -----
intro_callout: >
  **Prospective students, collaborators, and visitors are welcome.** The
  fastest way to reach us is by email — please read the **Join the Lab**
  section below before applying.

# ----- Principal Investigator card -----
pi:
  name: "Dr. Golmar Golmohammadi"
  role: "Assistant Professor — Watershed Hydrology and Biogeochemistry"
  affiliation: "UF/IFAS Range Cattle Research and Education Center (RCREC)"
  email: "g.golmohammadi@ufl.edu"
  phone: "(863) 374-7053"
  phone_tel: "+18633747053"
  address: "3401 Experiment Station, Ona, FL 33865"
  buttons:
    - { label: "Email Dr. Golmohammadi", url: "mailto:g.golmohammadi@ufl.edu", icon: "fas fa-envelope", style: "primary" }
    - { label: "Call the lab", url: "tel:+18633747053", icon: "fas fa-phone" }
    - { label: "UF/IFAS faculty page", url: "https://soils.ifas.ufl.edu/people/faculty/golmar-golmohammadi/", icon: "fas fa-id-card" }

# ----- Map (just type an address; the embed is built for you) -----
map:
  address: "3401 Experiment Station, Ona, FL 33865"
  zoom: 15

# ----- Find us: RCREC building + affiliated units (structured; edited in CMS) -----
find_us:
  building:
    name: "RCREC main building"
    lines:
      - "3401 Experiment Station"
      - "Ona, FL 33865"
    image: assets/img/rcrec-building.jpg
    buttons:
      - label: "Open in Google Maps"
        icon: "fas fa-map-marker-alt"
        url: "https://www.google.com/maps/search/?api=1&query=3401+Experiment+Station+Ona+FL+33865"
        ghost: false
      - label: "RCREC website"
        icon: "fas fa-external-link-alt"
        url: "https://rcrec-ona.ifas.ufl.edu/"
        ghost: true
  affiliations:
    - name: "Department of Soil, Water, and Ecosystem Sciences"
      short: "SWES"
      image: assets/img/affiliations/swes.jpg
      is_logo: false
      url: "https://soils.ifas.ufl.edu/"
      icon: "fas fa-flask"
    - name: "Department of Agricultural and Biological Engineering"
      short: "ABE"
      image: assets/img/affiliations/abe-frazier-rogers.jpg
      is_logo: false
      url: "https://abe.ufl.edu/"
      icon: "fas fa-cogs"
    - name: "UF Water Institute"
      short: "Water Institute"
      image: assets/img/affiliations/water-institute.png
      is_logo: true
      url: "https://waterinstitute.ufl.edu/"
      icon: "fas fa-water"

# ----- "Follow the lab" links -----
follow_links:
  - { label: "@WaterHydroLab", url: "https://x.com/WaterHydroLab", icon: "fab fa-x-twitter" }
  - { label: "GitHub", url: "https://github.com/waterhydrolab", icon: "fab fa-github" }
  - { label: "LinkedIn", url: "https://www.linkedin.com/in/golmar-golmohammadi-35791a17/", icon: "fab fa-linkedin" }
  - { label: "ORCID", url: "https://orcid.org/0000-0001-5532-3892", icon: "fab fa-orcid" }
  - { label: "Google Scholar", url: "https://scholar.google.com/citations?user=cpXxmlYAAAAJ", icon: "fas fa-graduation-cap" }
  - { label: "ResearchGate", url: "https://www.researchgate.net/profile/Golmar-Golmohammadi", icon: "fab fa-researchgate" }
  - { label: "RSS", url: "/feed.xml", icon: "fas fa-rss", style: "ghost" }

# ----- "Join the Lab" buttons -----
join_buttons:
  - {
      label: "Email a prospective-student inquiry",
      url: "mailto:g.golmohammadi@ufl.edu?subject=Prospective%20student%20inquiry%20%E2%80%94%20Watershed%20Hydrology%20Lab",
      icon: "fas fa-paper-plane",
      style: "primary",
    }
  - { label: "SWES graduate admissions", url: "https://soils.ifas.ufl.edu/academics/", icon: "fas fa-user-graduate" }
  - { label: "ABE graduate admissions", url: "https://abe.ufl.edu/graduate/", icon: "fas fa-user-graduate" }

# ----- "Postdoc & collaborator" buttons -----
postdoc_buttons:
  - {
      label: "Email a collaboration inquiry",
      url: "mailto:g.golmohammadi@ufl.edu?subject=Collaboration%20inquiry%20%E2%80%94%20Watershed%20Hydrology%20Lab",
      icon: "fas fa-handshake",
      style: "primary",
    }
  - { label: "See current research themes", url: "/projects/", icon: "fas fa-flask", style: "ghost" }
---

{% include whl_callout.liquid text=page.intro_callout %}

### Principal Investigator

{% include whl_pi_card.liquid %}

### Find us

{% include whl_map.liquid map=page.map %}

{% include whl_find_us.liquid %}

### Follow the lab

{% include whl_buttons.liquid items=page.follow_links %}

### Join the Lab

The lab welcomes **prospective Ph.D. and M.S. students** with backgrounds
in hydrology, water resources, agricultural and biological engineering,
soil and water sciences, environmental science, civil engineering, or
related fields. Strong programming (Python / R) and quantitative skills
are valued, as is curiosity for fieldwork at RCREC and the DeLuca Preserve.

**Before you email**, please:

1. Skim the [research themes](/projects/) to see if our work aligns with
   your interests.
2. Read a few of our [recent publications](/publications/) to understand
   the methods we use day-to-day.
3. Look at the [people page](/people/) and consider who you would
   collaborate with most closely.

When you write, include:

- A short paragraph introducing yourself and your research interests.
- Your **CV / résumé** (PDF).
- Your **transcripts** (unofficial is fine for a first contact).
- Optional: a writing sample (thesis chapter, conference paper, or
  technical report).

{% include whl_buttons.liquid items=page.join_buttons %}

### Postdoc & collaborator inquiries

Postdoctoral, visiting-scholar, and collaborative-research inquiries are
also welcome. Please email Dr. Golmohammadi directly with a brief
description of the proposed project, your CV, and (where relevant) a
sample of recent work.

{% include whl_buttons.liquid items=page.postdoc_buttons %}
