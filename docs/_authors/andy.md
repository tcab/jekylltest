---
short_name: andy
name: Andy Bulka
position: Chief Editor
my_number: 3
---
Andy is an avid programmer based in Australia.
The bio looping number is {{ page.my_number }}

<!-- this doesn't run?  -->
{% for n in page.my_number %}
    {{ n }} more bio info... 
{% endfor %}

<!-- this does run   -->
All posts:
{% for post in site.posts %}
* a site {{post.title}}
{% endfor %}
