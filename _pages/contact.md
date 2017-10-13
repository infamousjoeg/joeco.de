---
permalink: /contact/
title: "Hit Joe Up"
---

<form id="cntctfrm" method="POST">
    <input type="text" name="name" placeholder="Name">
    <input type="email" name="_replyto" placeholder="email@website.com">
    <input type="hidden" name="_subject" value="Website Contact" />
    <textarea name="message" placeholder="Message"></textarea>
    <input type="hidden" name="_next" value="//git.joeco.de/infamousjoeg.github.io-dev" />
    <input type="text" name="_gotcha" style="display:none" />
    <input type="submit" name="send" value="Send">
</form>
<script>
    var contactform = document.getElementById('contactform');
    contactform.setAttribute('action', '//formspree.io/' + 'jo' + 'e' + '@' + 'jo' + 'e' + '-' + 'gar' + 'cia' + '.' + 'c' + 'om');
<script>