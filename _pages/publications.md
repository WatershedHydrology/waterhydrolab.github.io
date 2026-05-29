---
# =============================================================================
#  PUBLICATIONS  ( /publications/ )
# =============================================================================
#  This page is auto-generated from _bibliography/papers.bib via the
#  jekyll-scholar plugin. To add a paper, edit papers.bib directly.
#  The search bar (bib_search.liquid include below) lets visitors filter
#  by title, author, year, or keyword.
# =============================================================================
layout: page
permalink: /publications/
title: publications
description: Peer-reviewed publications by Dr. Golmar Golmohammadi and the Watershed Hydrology Lab, in reverse chronological order.
nav: true
nav_order: 5

# ----- Buttons above the publication list (edited in the CMS, no HTML) -----
top_buttons:
  - { label: "Google Scholar", url: "https://scholar.google.com/citations?user=cpXxmlYAAAAJ", icon: "fas fa-graduation-cap", style: "primary" }
  - { label: "ORCID", url: "https://orcid.org/0000-0001-5532-3892", icon: "fab fa-orcid" }
  - { label: "ResearchGate", url: "https://www.researchgate.net/profile/Golmar-Golmohammadi", icon: "fab fa-researchgate" }
  - { label: "RSS", url: "/feed.xml", icon: "fas fa-rss" }
  - {
      label: "Request a reprint",
      url: "mailto:g.golmohammadi@ufl.edu?subject=Reprint%20request%20%E2%80%94%20Watershed%20Hydrology%20Lab",
      icon: "fas fa-envelope",
      style: "ghost",
    }
# ----- Buttons below the publication list -----
bottom_buttons:
  - { label: "Research themes", url: "/projects/", icon: "fas fa-flask" }
  - { label: "Meet the team", url: "/people/", icon: "fas fa-users" }
  - { label: "Contact", url: "/contact/", icon: "fas fa-paper-plane", style: "primary" }
---

{% include whl_buttons.liquid items=page.top_buttons %}

{% include bib_search.liquid %}

{% include whl_bibliography.liquid %}

{% include whl_buttons.liquid items=page.bottom_buttons %}
