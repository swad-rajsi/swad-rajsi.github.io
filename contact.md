---
layout: default
title: "Contact"
permalink: /contact/
---
<!-- 
<div style="color: #d25fd2ff;font-size:1.5em;font-family:Georgia;">Contact Us
</div> -->
<div class="swad-rajsi-centre-display" style="marging-left:2em;margin-right:2em;font-size:1em;font-family:sans-serif;color:darkslategray;padding:0.5em;">
You can send us a message or share a quick recipe with us !
</div>

<form id="contactMeForm" class="swad-rajsi-centre-display contact-form" action="https://formspree.io/f/mwveowlq" method="POST">
<div class="contact-me-form-group">
<label for="contactMeName">Name</label>
<input id="contactMeName" name="name" aria-multiline="false" role="textbox" type="name" class="contact-me-underline-input" value>
</div>
<div class="contact-me-form-group">
<label for="contactMeEmail">Email Address *</label>
<input id="contactMeEmail" name="email" aria-multiline="false" role="textbox" type="email" class="contact-me-underline-input" required value oninvalid="this.setCustomValidity('Please enter a valid email address.')" oninput="this.setCustomValidity('')">
</div>
<div class="contact-me-form-group">
<textarea id="contactMeMessage" name="message" rows="10" type="meassage"  class="contact-me-message-box contact-me-underline-input" required placeholder="Message"></textarea>
</div>

<div style="padding-left:40px;padding-right:40px;padding-bottm:50px;display:flex;justify-content:center;align-items:center;"><button type="submit" class="swad-rajsi-read-now" style="background-color:#d25fd2ff !important;border-width:0px;" >SEND</button></div>
</form>


<div class="swad-rajsi-centre-display" style="margin-top:5px;text-transform:none;">
<p id="contactMeSuccess" class="joining-mailing-list-success" style="display:none;">
✅ Thanks for contacting us! We will get back to you soon!!
</p>
<p id="contactMeError" class="joining-mailing-list-error" style="display:none;">
❌ Oops! Something went wrong. Please try again.
</p>
</div>

<script>
const form = document.getElementById('contactMeForm');
const contactMeName = document.getElementById('contactMeName');
const contactMeEmail = document.getElementById('contactMeEmail');
const contactMeMessage = document.getElementById('contactMeMessage');
const successMsg = document.getElementById('contactMeSuccess');
const errorMsg = document.getElementById('contactMeError');

contactMeMessage.addEventListener('blur', function() {
    // This resets the internal scroll of the textarea to the top
    this.scrollTo({
      top: 0,
      behavior: 'smooth'
    });
  });

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
successMsg.scrollIntoView({ behavior: 'smooth', block: 'center' });
contactMeName.value = "";
contactMeEmail.value = "";
contactMeMessage.value = "";
} else {
errorMsg.style.display = 'block';
successMsg.style.display = 'none';
errorMsg.scrollIntoView({ behavior: 'smooth', block: 'center' });
}
})
.catch(() => {
errorMsg.style.display = 'block';
successMsg.style.display = 'none';
});
});
</script>


<!-- 
# Contact Me

Email: yourname@example.com  

Instagram: [@yourhandle](https://instagram.com) -->
