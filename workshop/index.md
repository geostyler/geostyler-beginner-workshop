---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

{% for chapter in site.data.content %}
    {% capture my_include %}{% include_relative {{chapter.url}} %}{% endcapture %}
    {{ my_include | markdownify }}
{% endfor %}