---
layout: default
title: "Home"
---
<table style="background-color: #f7b7f0ff; height:100%;width:100%;">
<tr>
<td style="width:60%; vertical-align:top;background-color: #f7b7f0ff;"><img src="/assets/images/Cover.png" alt="Cover" width="100%"></td>
<td style="width:50%; vertical-align:top;background-color: #f7b7f0ff;">
  <div class="swad-rajsi-centre-display" style="padding-left:40px;padding-right:40px;padding-top:50px;">
  <p style="font-size:32px; font-style:oblique;font-family:cursive;">Explore delicious vegetarian recipes, modern twists, and quick meals</p>
  </div>
  <div class="swad-rajsi-centre-display" style="padding-left:40px;padding-right:40px;padding-bottm:50px;margin-top:-30px;">
  <p style="font-size:20px;">Join me in my love of food & cooking!</p>
  </div>
  <div class="swad-rajsi-centre-display" style="padding-left:40px;padding-right:40px;padding-bottm:50px;"><a class="swad-rajsi-read-now" href="{{ '/recipes/' | relative_url }}">READ NOW</a></div>
</td>
</tr>
</table>

<div class="swad-rajsi-centre-display" style="margin-top:30px;margin-bottom:10px;color: #d25fd2ff;font-size:32px;font-family:Georgia;" >
Welcome
</div>
<div class="swad-rajsi-centre-display" style="marging-left:30px;margin-right:30px;padding-left:100px;padding-right:100px;marging-bottom:30px;padding-bottom:20px;font-size:16px;font-family:sans-serif;color:darkslategray;">
There's much to see here. So, take your time, look around, and learn all there is to know about me. I love connecting with my readers. Let's share recipes and chat about our love for both traditional recipes and some new modern twists. I hope you enjoy my site and take a moment to say hello!
</div>
---
<div class="swad-rajsi-centre-display" style="margin-top:30px;margin-bottom:10px;color: #d25fd2ff;font-size:32px;font-family:Georgia;">Join My Mailing List
</div>
<div class="swad-rajsi-centre-display" style="marging-left:30px;margin-right:30px;padding-left:100px;padding-right:100px;font-size:16px;font-family:sans-serif;color:darkslategray;">
Be the first to hear about my latest recipes and food adventures!
</div>
<div>
<form id="joiningMailingListForm" class="swad-rajsi-centre-display" style="margin-top:30px;marging-left:20px;padding-left:40px;text-transform:none;" action="https://formspree.io/f/xqarjooq" method="POST">
<input name="email" aria-multiline="false" role="textbox" type="email" style="border-style:solid;border-left-width:0px;border-right-width:0px;border-top-width:0px;border-bottom-width:1px;margin-right:10px;padding:8px;padding-top:23px;border-color:darkgray;width:45%;vertical-align:middle;color:darkslategray;transition: border-color 0.3s;font-size:18px;font-family: arial;" required placeholder="Email Address" value>
<span style="padding-left:40px;padding-right:40px;padding-bottm:50px;"><button type="submit" class="swad-rajsi-read-now" style="background-color:#d25fd2ff !important;border-width:0px;" >SIGN UP</button></span>
</form>
</div>
<div class="swad-rajsi-centre-display" style="margin-top:5px;text-transform:none;">
<p id="joiningMailingListSuccess" class="joining-mailing-list-success" style="display:none;">
✅ Thanks for subscribing! You’ll receive delicious updates soon.
</p>
<p id="joiningMailingListError" class="joining-mailing-list-error" style="display:none;">
❌ Oops! Something went wrong. Please try again.
</p>
</div>

<script>
const form = document.getElementById('joiningMailingListForm');
const successMsg = document.getElementById('joiningMailingListSuccess');
const errorMsg = document.getElementById('joiningMailingListError');

form.addEventListener('submit', function(e) {
e.preventDefault();

fetch(form.action, {
method: 'POST',
body: new FormData(form),
headers: {
'Accept': 'application/json'
}
})
.then(response => {
if (response.ok) {
form.style.display = 'none';
successMsg.style.display = 'block';
errorMsg.style.display = 'none';
} else {
errorMsg.style.display = 'block';
successMsg.style.display = 'none';
}
})
.catch(() => {
errorMsg.style.display = 'block';
successMsg.style.display = 'none';
});
});
</script>

<!-- 
👉 Browse all **[Recipes](/recipes/)**  
👉 Learn more **[About Me](/about/)**  
👉 Get in touch **[Contact](/contact/)** 

---

## Latest Recipes

<ul>
  {% for recipe in site.recipes %}
    <li>
      <a href="{{ recipe.url }}">{{ recipe.title }}</a>
    </li>
  {% endfor %}
</ul>
-->
