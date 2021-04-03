# Notes - 教學
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
  <li>
    <a href="https://cypresslin.gitbooks.io/rolleiflex-622-repair/content/">維修紀錄 - Rolleiflex 622 K2 維修日誌</a>
  </li>
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
  <li>
    <a href="https://cypresslin.gitbooks.io/rolleiflex-622-repair/content/">維修紀錄 - Rolleiflex 622 K2 維修日誌</a>
  </li>
</ul>
