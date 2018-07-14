# ការពញ្ចូលទិន្ន័ទៅកាន់ Google form ពីវែបសាយផ្ទាល់ខ្លួន
# Submit Google Form From You Own Website

---
#### Simple Ajax Post is Credit to:
***Please read this first**
[https://github.com/jsdevel/google-form](https://github.com/jsdevel/google-form)

**Client site form validations**

index.html
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="description" content="">
    <meta name="author" content="">
    <title>Customize Google Form and Submit from your own website.</title>
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.2/css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body>
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <h1>Submit Google Form From Your Own Website.</h1>
        </div>
      </div>
      <div class="row">
          <div class="col-lg-12">
            <form
            id="contactForm"
            name="sentMessage"
            role="form"
            data-toggle="validator"
            method="POST"
            action="docs.google.com/forms/d/1zgLcOM0-Tle9CI5RjA67FgxGrYR_q95r-OiVZaeFXzE"
            onsubmit="return window.submitGoogleForm(this);">
              <div class="row">
                <div class="col-md-6">
                  <div class="form-group">
                    <input required name="entry.864873238" class="form-control" id="name" type="text" placeholder="Your Name *" >
                    <p class="help-block text-danger with-errors"></p>
                  </div>
                  <div class="form-group">
                    <input required  name="entry.1741846277" class="form-control" id="email" type="email" placeholder="Your Email *">
                    <p class="help-block text-danger with-errors"></p>
                  </div>
                  <div class="form-group">
                    <input name="entry.101984657" class="form-control" id="phone" type="tel" placeholder="Your Phone">
                    <p class="help-block text-danger with-errors"></p>
                  </div>
                  <div class="form-group">
                    <textarea required name="entry.769766787" class="form-control" id="message" placeholder="Your Message *"></textarea>
                    <p class="help-block text-danger with-errors"></p>
                  </div>
                  <div id="success"></div>
                  <button id="sendMessageButton" class="btn btn-primary btn-xl text-uppercase" type="submit">Send Message</button>
                </div>
              </div>
            </form>
          </div>
        </div>
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.2/js/bootstrap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/1000hz-bootstrap-validator/0.11.9/validator.min.js"></script>
    <script src='js/submit-google-form.js'></script>
  </body>
</html>
```

submit-google-form.js
for this we do need to validate input  first if it's validated we submit if not we do nothing.

```js
!function(exports) {
  exports.submitGoogleForm = submitGoogleForm;
  function submitGoogleForm(form) {
    $('#contactForm').validator().on('submit', function (e) {
      if (e.isDefaultPrevented()) {
        // handle the invalid form...
      } else {
        try {
          var data = [].slice.call(form).map(function(control) {
            return 'value' in control && control.name ?
              control.name + '=' + (control.value === undefined ? '' : control.value) :
              '';
          }).join('&');
          var xhr = new XMLHttpRequest();

          xhr.open('POST', form.action + '/formResponse', true);
          xhr.setRequestHeader('Accept',
              'application/xml, text/xml, */*; q=0.01');
          xhr.setRequestHeader('Content-type',
              'application/x-www-form-urlencoded; charset=UTF-8');
          xhr.send(data);
        } catch(e) {}

        form.parentNode.className += ' submitted';
        // document.getElementById("contactForm").reset();
        window.location.href = window.location.href
        return false;

      }
    })
  }

}(typeof module === 'undefined' ? window : module.exports);

```
