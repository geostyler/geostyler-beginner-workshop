
---

# Imprint

This workshop is licensed under the [CC BY-SA](http://creativecommons.org/licenses/by-sa/2.0/) license. If you have questions, you can contact us
on GitHub [@terrestris](https://github.com/terrestris), via E-Mail [info@terrestris.de](mailto:info@terrestris.de), [reports@geostyler.org](mailto:reports@geostyler.org) or via telephone 0228 – 962 899 51.

## Authors

{% for author in site.data.vars.authors %}
  - {{ author.name }} ([{{ author.mail }}](mailto:{{ author.mail }}))
{% endfor %}
