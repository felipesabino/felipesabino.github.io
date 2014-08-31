---
layout:     post
title:      Javascript – Checking the file size
date:       2012-01-30 10:00:00
summary:    Using JavaScript to check the file size before uploading
categories: javascript
---

It is true that Javascript has no access to your File System.

[http://en.wikipedia.org/wiki/JavaScript#Security](http://en.wikipedia.org/wiki/JavaScript#Security)

> JavaScript and the DOM provide the potential for malicious authors to deliver scripts to run on a client computer via the web. Browser authors contain this risk using two restrictions. First, scripts run in a sandbox in which they can only perform web-related actions, not general-purpose programming tasks like creating files

However, the HTML5 File API specification, [compatible with current modern browsers](http://caniuse.com/#feat=fileapi) ([IE 9- excluded, obviously](http://people.mozilla.com/~prouget/ie9/)), finally allows a standard interaction with local files.

For example, you could get the selected file size as the following

For the HTML bellow

{% highlight html %}
<input type="file" id="myFile" />
Here is the Javascript code to alert the file size every time the user selects a different file.
{% endhighlight %}
{% highlight javascript %}
//gets the element by its id
var myFile = document.getElementById('myFile');

//binds to onchange event of the input field
myFile.addEventListener('change', function() {
  //this.files[0].size gets the size of your file.
  alert(this.files[0].size);

});
{% endhighlight %}

In the example above, this.files exposes a [FileList](http://www.w3.org/TR/FileAPI/#dfn-filelist) object, which is an array-like object of File objects.

As described by the [File’s object HTML specification](http://www.w3.org/TR/FileAPI/#dfn-file) here are some other file properties you could retrieve.

- `name`: Returns a string containing the file name (without the path information)
- `lastModifiedDate`: Returns a Date object that represents the file last modified date
- `size`: Returns an integer representing the file size in bytes
- `type`: Returns a string with the file [MIME type](https://en.wikipedia.org/wiki/Internet_media_type)

This is a perfect solution for improving user experience while implementing file uploads and avoiding having to submit the file to have this kind of check only at the server side.

Other useful resources:

[http://html5-demos.appspot.com/static/gdd11-modern-web-apps/index.html](http://html5-demos.appspot.com/static/gdd11-modern-web-apps/index.html)

[http://stackoverflow.com/questions/4349144/will-ie9-support-the-html5-file-api](http://stackoverflow.com/questions/4349144/will-ie9-support-the-html5-file-api)

---

Originally posted by me at [http://i.ndigo.com.br/2012/01/javascipt-checking-the-file-size](https://web.archive.org/web/20130724051813/http://i.ndigo.com.br/2012/01/javascipt-checking-the-file-size)
