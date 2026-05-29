---
# =============================================================================
#  NEWS  ( /news/ )
# =============================================================================
#  The page lists every file in /_news/ in reverse-chronological order.
#  To post a news item:
#    - Create /_news/announcement_<NUM>.md
#    - Use this front matter:
#        ---
#        layout: post
#        date: YYYY-MM-DD HH:MM:SS-0500     # set the post date
#        inline: true                       # set false for a full post page
#        related_posts: false
#        ---
#        Your announcement text (markdown).
#  The five most recent items also appear on the homepage strip.
# =============================================================================
layout: page
title: news
permalink: /news/
description: Lab announcements, publications, grants, and student milestones.
nav: true
nav_order: 6

# ----- Buttons under the news list (edited in the CMS, no HTML) -----
footer_buttons:
  - { label: "Subscribe via RSS", url: "/feed.xml", icon: "fas fa-rss", style: "primary" }
  - { label: "Follow @WaterHydroLab", url: "https://x.com/WaterHydroLab", icon: "fab fa-x-twitter" }
  - { label: "GitHub", url: "https://github.com/waterhydrolab", icon: "fab fa-github" }
  - { label: "LinkedIn", url: "https://www.linkedin.com/in/golmar-golmohammadi-35791a17/", icon: "fab fa-linkedin" }
  - { label: "Contact the lab", url: "/contact/", icon: "fas fa-paper-plane", style: "ghost" }
---

{% include whl_news.liquid %}

{% include whl_buttons.liquid items=page.footer_buttons %}
