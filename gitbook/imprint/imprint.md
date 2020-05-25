# Imprint

Dieser Workshop ist unter der Lizenz [CC BY-SA](http://creativecommons.org/licenses/by-sa/2.0/) lizenziert. Bei Fragen können Sie sich gerne über GitHub [@terrestris](https://github.com/terrestris), E-Mail [info@terrestris.de](mailto:info@terrestris.de) oder Telefon 0228 – 962 899 51 an uns wenden.

## Authoren

{% for author in book.authors %}
  - {{ author.name }} ([{{ author.mail }}](mailto:{{ author.mail }}))
{% endfor %}