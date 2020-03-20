---
layout: default
title: About
my_number: 3
---
# About page

This page tells you a little bit about me.
OKOK

<!-- this doesn't run?  -->
{% for n in page.my_number %}
    <p> 
    {{ n }} more ABOUT info... 
    </p>
{% endfor %}