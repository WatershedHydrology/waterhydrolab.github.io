---
# =============================================================================
#  FACILITIES  ( /facilities/ )
# =============================================================================
#  Field-instrumentation network at RCREC and the DeLuca Preserve plus the
#  RCREC Hydrology Lab equipment, shown as a map + instrument cards + a media
#  gallery.
#
#  EDITING IN THE CMS (Other Pages -> Facilities):
#    - "Instruments", "Lab equipment", and "Field Gallery" are STRUCTURED.
#      Each instrument/equipment item has a Name, a Meta line (site · years), a
#      Description, and one or more Photos (click-to-upload). The Field Gallery
#      is a list where each item is a photo OR a video (click-to-upload), or a
#      pasted YouTube/Vimeo embed. Add / remove / reorder items there — no HTML.
#      One photo = full-width; two or more = a thumbnail grid.
#    - "Map" is just an address (the embed is built for you) and "Visit /
#      Tour buttons" is a button list. Only the intro paragraph and the
#      section headings stay in "Page content".
# =============================================================================
layout: page
permalink: /facilities/
title: facilities
description: Field instrumentation and laboratory equipment supporting hydrologic and water-quality research at RCREC and the DeLuca Preserve.
nav: true
nav_order: 4

# ----- Field Instrumentation (structured cards; edited in the CMS) -----
instruments:
  - name: "Hydrometric Station — SonTek acoustic Doppler flow meter"
    meta: "RCREC & DeLuca Preserve · 2023–present"
    description: "Continuously measures stream and open-channel discharge, velocity, water level, flow direction, temperature, and diagnostic quality metrics."
    images:
      - assets/img/instruments/sontek.jpg
      - assets/img/instruments/sontek-2.jpg
      - assets/img/instruments/sontek-3.jpg
      - assets/img/instruments/sontek-4.jpg
  - name: "Weather Station"
    meta: "RCREC · 2024–present"
    description: "Air temperature, humidity, rainfall, wind, and solar radiation, logged for real-time remote monitoring."
    images:
      - assets/img/instruments/weather-station.jpg
  - name: "Lysimeter"
    meta: "RCREC · 2024–present"
    description: "Tracks water movement through the soil profile and collects percolated water to quantify subsurface drainage and solute (e.g., nitrate) leaching."
    images:
      - assets/img/instruments/lysimeter.jpg
  - name: "Zentra ZL6 Data Logger"
    meta: "RCREC · 2024–present"
    description: "Records data from TEROS-series and EC-5 sensors and transmits to the ZENTRA Cloud."
    images:
      - assets/img/instruments/zentra-zl6.jpg
      - assets/img/instruments/zentra-zl6-2.jpg
  - name: "Groundwater Wells — Rugged TROLL sensors"
    meta: "RCREC (5 wells) & DeLuca Preserve (3 wells) · 2023–present"
    description: "Continuous logging of groundwater level and temperature."
    images:
      - assets/img/instruments/rugged-troll.jpg
      - assets/img/instruments/rugged-troll-2.jpg
  - name: "Aqua TROLL Sonde"
    meta: "RCREC · 2023–present"
    description: "Multi-parameter water-quality sonde: level, temperature, pH, dissolved oxygen, electrical conductivity, and turbidity."
    images:
      - assets/img/instruments/aqua-troll.jpg
  - name: "VuLink Data Logger"
    meta: "DeLuca Preserve · 2024–present"
    description: "Automated data logging and wireless transmission for groundwater-level sensors."
    images:
      - assets/img/instruments/vulink.jpg
  - name: "TEROS 12 — Soil-Moisture Sensor"
    meta: "RCREC · 2024–present"
    description: "Capacitance-based volumetric water content, temperature, and electrical conductivity."
    images:
      - assets/img/instruments/teros-12.jpg
  - name: "TEROS 54 — Soil-Moisture Profile Probe"
    meta: "RCREC · 2024–present"
    description: "Multi-depth soil water potential and temperature."
    images:
      - assets/img/instruments/teros-54.jpg
  - name: "Onset ECH₂O EC-5 — Soil-Moisture Sensor"
    meta: "RCREC · 2025–present"
    description: "Volumetric water content via capacitance-based dielectric measurement."
    images:
      - assets/img/instruments/ec-5.jpg

# ----- Laboratory Equipment (structured cards; edited in the CMS) -----
lab_equipment:
  - name: "Benchtop Multiparameter Meter"
    meta: "RCREC Hydrology Lab · 2026–present"
    description: "Measures pH, electrical conductivity, and temperature in water and soil samples."
    images:
      - assets/img/instruments/benchtop-meter.jpg
      - assets/img/instruments/benchtop-meter-2.jpg
  - name: "AQ300 Discrete Analyzer"
    meta: "RCREC Hydrology Lab · 2026–present"
    description: "Automated nutrient and chemical analysis (nitrate, ammonia, phosphate) of water, wastewater, and soil samples via robotic sampling and spectrophotometry."
    images:
      - assets/img/instruments/aq300.jpg
      - assets/img/instruments/aq300-2.jpg
      - assets/img/instruments/aq300-3.jpg

# ----- Field Gallery (videos / photos / embeds; edited in the CMS) -----
gallery:
  - file: /assets/video/video_1.mp4
  - file: /assets/video/video_2.mp4

# ----- Map (just type an address; the embed is built for you) -----
map:
  address: "3401 Experiment Station, Ona, FL 33865"
  zoom: 13

# ----- Buttons under "Visit, Tour, or Partner" (edited in the CMS, no HTML) -----
visit_buttons:
  - {
      label: "Request a tour or data",
      url: "mailto:g.golmohammadi@ufl.edu?subject=Lab%20tour%20%2F%20facilities%20inquiry%20%E2%80%94%20Watershed%20Hydrology%20Lab",
      icon: "fas fa-envelope",
      style: "primary",
    }
  - { label: "RCREC website", url: "https://rcrec-ona.ifas.ufl.edu/", icon: "fas fa-external-link-alt" }
  - {
      label: "Directions to RCREC",
      url: "https://www.google.com/maps/search/?api=1&query=3401+Experiment+Station+Ona+FL+33865",
      icon: "fas fa-map-marker-alt",
    }
  - { label: "Research themes", url: "/projects/", icon: "fas fa-flask" }
  - { label: "Contact", url: "/contact/", icon: "fas fa-paper-plane", style: "ghost" }
---

A comprehensive suite of field instruments is deployed across research sites at
the **Range Cattle Research and Education Center (RCREC)** and the **DeLuca
Preserve** to collect high-resolution data on hydrological, soil, forage, and
atmospheric conditions. Weather stations, soil-moisture sensors, lysimeters,
groundwater wells, surface-water flow meters, and water-quality sondes feed
data loggers and telemetry systems for continuous, remotely accessible
monitoring — supporting detailed water-balance and water-quality analyses. The
**RCREC Hydrology Laboratory** then analyzes the collected soil, water, and
forage samples.

## Where We Work

{% include whl_map.liquid map=page.map %}

## Field Instrumentation

{% include whl_card_grid.liquid items=page.instruments %}

## Laboratory Equipment

{% include whl_card_grid.liquid items=page.lab_equipment %}

## Field Gallery

{% include whl_gallery.liquid %}

## Visit, Tour, or Partner With the Lab

{% include whl_buttons.liquid items=page.visit_buttons %}
