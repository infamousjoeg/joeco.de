---
permalink: /contact/
title: "Hit Joe Up"
---

<form id="cntctfrm" method="POST">
    <div class="input group margin-bottom-sm">
        <span class="input-group-addon"><i class="fa fa-user-circle-o fa-fw"></i></span>
        <input class="form-control" type="text" name="name" placeholder="Your Name">
    </div>
    <div class="input group margin-bottom-sm">
        <span class="input-group-addon"><i class="fa fa-envelope-o fa-fw"></i></span>
        <input class="form-control" type="email" name="_replyto" placeholder="you@example.com">
    </div>
    <textarea name="message" placeholder="Message"></textarea>
        <input type="hidden" name="_subject" value="Website Contact" />
    <input type="hidden" name="_next" value="//joeco.de" />
    <input type="text" name="_gotcha" style="display:none" />
    <button type="submit" name="submit" class="btn btn-lg btn-success"><i class="fa fa-paper-plane fa-2x pull-left"></i> Send Message<br>To Joe G</button>
</form>
<script>
    var contactform = document.getElementById('contactform');
    contactform.setAttribute('action', '//formspree.io/' + 'jo' + 'e' + '@' + 'jo' + 'e' + '-' + 'gar' + 'cia' + '.' + 'c' + 'om');
<script>
