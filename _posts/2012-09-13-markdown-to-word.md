---
layout: post
title: Convert Markdown to Word
description: How to convert a markdown file into a fully useable Word Document
---

### Using Pandoc

Converting a Markdown file to a Word document with pandoc is really easy. All you need to do is to get [pandoc](http://johnmacfarlane.net/pandoc/) version 1.9 or higher, then:

{% highlight sh %}
pandoc myfile.txt -o myfile.docx
{% endhighlight %}    

That will take the file myfile.txt and convert it to the Word document myfile.docx.

### Using Google Docs

If you don't want to install pandoc for some reason, you can also use Google Docs. Convert your Markdown file to HTML, then upload it to Google Docs, select the option for Google Docs to convert it to their format, then download it as a DOC file.