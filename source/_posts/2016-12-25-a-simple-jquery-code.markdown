---
layout: post
title: "A simple jQuery code"
date: 2016-12-25 21:39:57 +0800
comments: true
categories: jQuery
---
<!-- more -->
``` html
<li class="confirmation">
  <h3>Hawaiian Vacation</h3>
  <button>Flight details</button>
  <div class="ticket">
    <a class="view-boarding-pass">View Boarding Pass</a>
    <img src="/ticket-14836.png" />
  </div>
</li>
```

``` js
$('.confirmation').on('click','button', function(){
  $(this).find('.ticket').slideDown();
});

$('.confirmation .view-boarding-pass').on('click', function(){
  $(this).closest('ticket').find('img').show();
});
```

But, If we need makeing a Ajax call.

``` js
$('.confirmation').on('click','button', function(){
  $.ajax('http://example.org/confirmation.html', {
    success: function(response) {
      $('.ticket').html(response).slideDown();
    }
  )};
});
// or $.ajax('confirmation.html')
```

Shorthand with $.get

``` js
$.get('confirmation.html', function(response) {
  $('.ticket').html(response).slideDown();
});
```

### Sending parameters with requests

like this `confirmation.html?confNum=1234`

``` js
  $.ajax('http://example.org/confirmation.html', {
    success: function(response) {
      $('.ticket').html(response).slideDown();
    },
    data: { "confNum": 1234 }
  )};
```

### Pulled from the HTML

``` html
<div class='ticket' data-confNum='1234'>
```

``` js
  $.ajax('http://example.org/confirmation.html', {
    success: function(response) {
      $('.ticket').html(response).slideDown();
    },
    data: { "confNum": $("ticket").data("confNum") }
  )};
```
