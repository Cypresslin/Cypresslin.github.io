## /dev/random

# Notes - 長篇大論
<ul>
  <li>
    <a href="https://cypresslin.github.io/book-mm5-101/">MM5 101</a>
  </li>
</ul>

# Notes - Electronics
<ul>
  {% for post in site.categories.electronics %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

# Minister of Disassembly - 親拆大臣
<ul>
  {% for post in site.categories.MinisterOfDisassembly %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

# All Notes
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
  <li>
    <a href="https://cypresslin.github.io/book-mm5-101/">MM5 101</a>
  </li>
</ul>
