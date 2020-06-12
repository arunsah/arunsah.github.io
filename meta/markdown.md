# Markdown Cheatsheet
📅 [2020-05-31](https://arunsah.github.io/meta/changelog#2020-05-31) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Pune, India](https://en.wikipedia.org/wiki/Hinjawadi)

---

## References:

- Emoji Cheat Sheet: [https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md)
- Markdown-Cheatsheet: [https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- Markdown Table Generator: [https://www.tablesgenerator.com/markdown_tables#](https://www.tablesgenerator.com/markdown_tables#)
- Relative Links In Markup Files: [https://github.blog/2013-01-31-relative-links-in-markup-files/](https://github.blog/2013-01-31-relative-links-in-markup-files/)
Turns into This is Blue italic.


###### Testing Mix-HTML for Github Page

- Coloured Text:

<span style="color:red">red color text</span>

- Javascript alert Text:

<span style="color:blue; width:200px; border:1px solid deepblue;" onclick="javascript:alert('end');">Blue Button</span>


<style>
.content {
  padding: 0 18px;
  background-color: white;
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.2s ease-out;
}
</style>

<script>
var coll = document.getElementsByClassName("collapsible");
var i;

for (i = 0; i < coll.length; i++) {
  coll[i].addEventListener("click", function() {
    this.classList.toggle("active");
    var content = this.nextElementSibling;
    if (content.style.maxHeight){
      content.style.maxHeight = null;
    } else {
      content.style.maxHeight = content.scrollHeight + "px";
    }
  });
}
</script>

<button type="button" class="collapsible">Open Collapsible</button>
<div class="content">
  <p>Lorem ipsum...</p>
</div>

