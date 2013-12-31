# EmailComposer with attachments handling

## Notice

*This plugin only works with Steroids 2.7.x. For Steroids 3.1.x, you should use https://github.com/jcjee/email-composer/ instead.*

## Plugin

[Plugman](https://github.com/apache/cordova-plugman)-compatible email composer plugin with attachements, combined from [EmailComposer Plugin for iOS](https://github.com/phonegap/phonegap-plugins/tree/master/iOS/EmailComposerWithAttachments) and [EmailComposer Plugin for Android](https://github.com/phonegap/phonegap-plugins/tree/master/Android/EmailComposerWithAttachments)

## Usage with Steroids

Download the `www/EmailComposer.js` file from this repo, and include it in your project (e.g. `www/plugins/EmailComposer.js`). Then, load the JavaScript file with a `<script>` tag:

```
<script src="/plugins/EmailComposer.js"></script>
```

Now, you should have `window.plugins.emailComposer` defined in your WebView.

### JavaScript API

There are two methods you can use to show the email composer window:

```
window.plugins.emailComposer.showEmailComposerWithCallback(callback,subject,body,toRecipients,ccRecipients,bccRecipients,isHtml,attachments);
```

or

```
window.plugins.emailComposer.showEmailComposer(subject,body,toRecipients,ccRecipients,bccRecipients,isHtml,attachments);
```

**Parameters:**
- callback: a JavaScript function that will receive return parameter from the plugin
- subject: a string representing the subject of the email; can be null
- body: a string representing the email body (could be HTML code, in this case set **isHtml** to **true**); can be null
- toRecipients: an array containing all the email addresses for TO field; can be null/empty
- ccRecipients: an array containing all the email addresses for CC field; can be null/empty
- bccRecipients: an array containing all the email addresses for BCC field; can be null/empty
- isHtml: a boolean value indicating if the body is HTML or plain text
- attachments: an array containing all full paths to the files you want to attach; can be null/empty (in format /var/mobile/...)

**Example**

```
var ops = {
  callback: function(result){console.log(result);},
  subject: "Look at this photo",
  body: "Take a look at <b>this</b>:"
  toRecipients: ["example@email.com", "johndoe@email.org"],
  ccRecipients: [],
  bccRecipients: [],
  isHTML: true,
  attachments: ["_complete_path/image.png"]
}

window.plugins.emailComposer.showEmailComposerWithCallback(ops.callback, ops.subject, ops.body, ops.toRecipients, ops.ccRecipients, ops.bccRecipients, ops.isHTML, ops.attachments);
```

**Return values for callback function**
- 0: email composition cancelled (cancel button pressed and draft not saved)
- 1: email saved (cancel button pressed but draft saved)
- 2: email sent
- 3: send failed
- 4: email not sent (something wrong happened)

### Installing the plugin

To use the EmailComposer plugin with Steroids, you need to create a custom Scanner (or Ad Hoc) build of your app using the AppGyver Build Serivce. See the instructions at http://guides.appgyver.com/steroids/guides/cloud_services/plugin-config/ for more information.

### Setting up config.xml

On iOS, in your Steroids project's `www/config.ios.xml`, add the following tag inside the `<plugins>` tag:

```
<plugin name="EmailComposer" value="EmailComposer" onload="true"/>
```

On Android, add to `www/config.android.xml` the tag:

```
<plugin name="EmailComposer" value="org.apache.cordova.EmailComposer"/>
```

##Known issues

Opening the email compose window from a modal window (opened via `steroids.modal.show()`) might cause errant behavior.

# LICENSE
The MIT License

Copyright (c) 2010 Jesse MacFadyen

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
