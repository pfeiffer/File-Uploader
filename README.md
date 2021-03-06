<h1>File Uploader</h1>

File Uploader is a flash-based file uploader, alternative to SWFUpload. It is robust, fast and easy to use. It is meant to be used on a web pages to replace standard &lt;input type="file" /&gt;.

<b>File Uploader is under development and it's implementation is experimental. No stable release is currently available. I am seeking for File Uploader testers. If you have downloaded File Uploader, tested it and found issues using it, please let me know what those issues were, I will fix the problem as soon as possible.</b>

<i>Why to create File Uploader when there are alternatives like <a href="http://www.swfupload.org">SWFUpload</a> available out there?</i><br />
File Uploader is inspired from SWFUpload. The problem with SWFUpload is that it is not optimized for usage on a web pages where you have lots of 'upload buttons' on single page. The kind of pages could be administration panels with some kind of category list, where in front of each category you have an icon, and that icon, when clicked, allows you to instantly replace it by uploading selected file from popped-up dialog window. When you use SWFUpload to do such things, the computer resource usage grows with each new upload button instance, because everytime you instantiate new SWFUpload object, SWFUpload embeds one more SWF file instance on to the page, this means that at the end you have as much SWF's (Flash players) running as 'upload buttons' you have. If you allocate too much buttons, the browser could crash because of lack of resources. To work around this problem i was trying to implement a solution where you mouseover an icon, you get a new SWFUpload instance immediately, and when mouseout the icon, SWFUpload instance is getting destroyed. This solution did not work a minute, because of a bug i described <a href="http://github.com/Evolver/browser-bugs/tree/master/flash/file-dialog-crash/">here</a>. The browser kept on crashing because of Flash &lt;OBJECT&gt; being removed from DOM while file dialog is open. Here is how File Uploader was born and what issues it is meant to solve.

<h2>What makes it great:</h2>

<ul>
  <li>Lighweight, <b>uses one SWF embed for all uploader instances</b> (buttons) on page.</li>
  <li>Supports <b>multiple file selection in one dialog window</b> and <b>parallel file uploading</b></li>
  <li>Supports <b>multiple uploaders (queues) per page</b> without impact on performance</li>
  <li>Supports <b>per-file POST arguments</b></li>
  <li>Provides many configuration settings to adjust File Uploader behavior to your needs</li>
  <li>Provides <b>transfer rate (speed) calculation</b> during file upload</li>
  <li>Allows you to use <b>any custom HTML as clickable 'upload button'</b></li>
  <li>Easy-to-use high level API out of box</li>
  <li>Exports low level API to create custom high level APIs</li>
  <li>Supports <b>automatic upload start</b></li>
  <li>Designed to <b>support any JavaScript library</b></li>
  <li>Code is <b>Open Source</b>, licensed under <a href="http://www.gnu.org/licenses/gpl-2.0.html">GPL v2</a></li>
</ul>

<h2>With File Uploader you can:</h2>

<ul>
  <li>Use any HTML code as clickable 'upload button'</li>
  <li>Select multiple files for uploading</li>
  <li>Upload selected files asynchronously (without submitting the form, just like AJAX works)</li>
  <li>Display upload progress bars</li>
  <li>Display transfer rates (uploading speed)</li>
  <li>Display file names, sizes and types</li>
  <li>Manipulate file upload queue</li>
  <li>Receive JSON or any other data from server as response</li>
  <li>Upload files to different URLs with different POST variables simultaneously</li>
</ul>

<h2>Installation and usage</h2>

<h3>Step 1 - Make a File Uploader bundle you need</h3>

To use File Uploader you have include four separate File Uploader source code parts in your webpage:

<ol>
  <li>Dependent library (such as jQuery, Prototype.js or something else) and it's binding for FileUploader [located in <b>src/js/dep/</b>]</li>
  <li>File Uploader core file [<b>src/js/fileUploader.core.js</b>]</li>
  <li>File Uploader public API file (API you will use to work with uploader) [located in <b>src/js/api/</b>]</li>
  <li>File Uploader SWF file [<b>bin/flash/FileUploader.swf</b>]</li>
</ol>

Or you can use a File Uploader bundle building tool <b>build/build.php</b>. Use this script from command line by running php.<br />

Usage:   <i>php build.php &lt;<b>source directory</b>&gt; &lt;<b>dependent library name</b>&gt; &lt;<b>output file name</b>&gt;</i><br />
Example: php build.php "C:\repo\File-Uploader" jQuery "fileUploader.jQuery.js"<br />

Note: currently only jQuery library API is supported.

<h3>Step 2 - Deploy File Uploader on your webserver</h3>

<ol>
  <li>Take the files you collected and deploy them on your webserver</li>
  <li>Make sure <b>fileUploader.core.js</b> is configured correctly and URL of File Uploader SWF file is correct</li>
  <li>Include <b>dependent library JS</b> code, include <b>dependent library File Uploader bindings</b>, include <b>fileUploader.core.js</b> and <b>File Uploader public API</b> file.
  
    Example:
    <pre>
  &lt;!-- dependent library and binding --&gt;
  &lt;script type="text/javascript" src="/src/js/dep/jQuery/jquery-1.3.2.js">&lt;/script&gt;
  &lt;script type="text/javascript" src="/src/js/dep/jQuery/fileUploader.jQuery.js">&lt;/script&gt;
  
  &lt;!-- uploader core file --&gt;
  &lt;script type="text/javascript" src="/src/js/fileUploader.core.js">&lt;/script&gt;
  
  &lt;!-- uploader public API --&gt;
  &lt;script type="text/javascript" src="/src/js/api/fileUploader.Uploader.js"&gt;&lt;/script&gt;
    </pre>
  </li>
</ol>

<h3>Step 3 - Use File Uploader</h3>

<b>To use out of box API, use the following code:</b>

<pre>
  &lt;!-- dependent library and binding --&gt;
  &lt;script type="text/javascript" src="/src/js/dep/jQuery/jquery-1.3.2.js">&lt;/script&gt;
  &lt;script type="text/javascript" src="/src/js/dep/jQuery/fileUploader.jQuery.js">&lt;/script&gt;
  
  &lt;!-- uploader core file --&gt;
  &lt;script type="text/javascript" src="/src/js/fileUploader.core.js">&lt;/script&gt;
  
  &lt;!-- uploader public API --&gt;
  &lt;script type="text/javascript" src="/src/js/api/fileUploader.Uploader.js"&gt;&lt;/script&gt;
</pre>

...

<pre>
  // Specify where your flash file (FileUploader.swf) resides.
  // This should be done once before any instantiation of fileUploader.Uploader object.
  fileUploader.config.swfUrl ='/flash/FileUploader.swf';
  
  // instantiate uploader
  var uploader =new fileUploader.Uploader({
    // url where to upload the file
    'url': 'http://www.example.com/upload.php',
    // file entry name
    'fileName': 'myFile',
    // POST arguments
    'postArgs': {'action':'upload','galleryId':15},
    '
  });
  
  // configure uploader (optional)
  uploader.concurrency =2;
  uploader.timeout =15;
  
  // listen to events
  
  // handle dialog open
  uploader.onDialogOpen =function() {
    
  };
  
  // handle file selection
  uploader.onSelect =function( id, fileInfo) {
    
  };
  
  // handle file removal
  uploader.onRemove =function( id, fileInfo) {
    
  };
  
  // handle dialog closure
  uploader.onDialogClose =function() {
    
  };
  
  // handle file uploading start
  uploader.onUploadStart =function( id, fileInfo) {
    
  };
  
  // handle file uploading progress
  uploader.onUploadProgress =function( id, fileInfo, bytesLoaded, bytesTotal, percComplete) {
    
  };
  
  // handle file uploading error
  uploader.onUploadError =function( id, fileInfo, errorMsg) {
    
  };
  
  // handle file uploading success
  uploader.onUploadSuccess =function( id, fileInfo, serverData, filesPending) {
    
  };
  
  // handle file uploading completion
  uploader.onUploadComplete =function( id, fileInfo, filesPending, removeFromQueue) {
    
  };
  
  // deploy
  uploader.attach( document.getElementById( 'myButton'));
</pre>

<b>jQuery API:</b>

<pre>
  &lt;!-- dependent library and binding --&gt;
  &lt;script type="text/javascript" src="/src/js/dep/jQuery/jquery-1.3.2.js">&lt;/script&gt;
  &lt;script type="text/javascript" src="/src/js/dep/jQuery/fileUploader.jQuery.js">&lt;/script&gt;
  
  &lt;!-- uploader core file --&gt;
  &lt;script type="text/javascript" src="/src/js/fileUploader.core.js">&lt;/script&gt;
  
  &lt;!-- uploader public API --&gt;
  &lt;script type="text/javascript" src="/src/js/api/fileUploader.Uploader.js"&gt;&lt;/script&gt;
  
  &lt;!-- jQuery public API binding --&gt;
  &lt;script type="text/javascript" src="/src/js/api/jQuery/fileUploader.jQuery.js"&gt;&lt;/script&gt;
</pre>

...

<pre>
  // Specify where your flash file (FileUploader.swf) resides.
  // This should be done once before any instantiation of fileUploader.Uploader object.
  fileUploader.config.swfUrl ='/flash/FileUploader.swf';
  
  // jQuery-wrapped #myButton
  var $btn =$( '#myButton');
  
  // listen to events
  $btn.bind( 'uploadDialogOpen uploadDialogClose uploadFileSelect uploadFileRemove uploadStart uploadProgress uploadSuccess uploadError uploadComplete', function( e, data){
    switch( e.type) {
      case 'uploadDialogOpen':
        debug( 'Dialog open');
      break;
      case 'uploadDialogClose':
        debug( 'Dialog close');
      break;
      case 'uploadFileSelect':
        debug( 'Select file #' +data.fileId +' - ' +data.fileInfo.name + ' (size=' +data.fileInfo.size +')');
      break;
      case 'uploadFileRemove':
        debug( 'Remove file #' +data.fileId +' - ' +data.fileInfo.name);
      break;
      case 'uploadStart':
        debug( 'Start upload #' +data.fileId +' - ' +data.fileInfo.name);
      break;
      case 'uploadProgress':
        debug( 'Upload progress #' +data.fileId +' - ' +data.fileInfo.name + ' (' +data.percComplete +'%)');
      break;
      case 'uploadSuccess':
        debug( 'Upload success #' +data.fileId +' - ' +data.fileInfo.name);
      break;
      case 'uploadError':
        debug( 'Upload error #' +data.fileId +' - ' +data.fileInfo.name +' (' +data.errorMsg +')');
      break;
      case 'uploadComplete':
        debug( 'Upload complete #' +data.fileId +' - ' +data.fileInfo.name);
      break;
    }
  });
  
  // initialize uploader
  var uploaderObject =$btn.uploader({
    'url': '/test/receive.php'
  });
  
  // optionally configure uploader instance
  //uploaderObject.concurrency =2;
  
  // detach uploader from a button
  //uploaderObject.detach();
</pre>

<h3>Examples</h3>

You can view live debugging preview of native API <a href="http://www.stepanov.lv/uploader/test/native.html">here</a>. jQuery version of File Uploader debug preview can be found <a href="http://www.stepanov.lv/uploader/test/jQuery.html">here</a>.

If you have cloned repo and trying to view tests from your local hard drive, the tests won't work because of Flash's security features. You have to upload tests to a web host and access them via browser to see File Uploader in action.

<h2>Supported browsers</h2>

File Uploader was tested and is working as expected in:

<ul>
  <li>Win32 Flash player 10.0.22+</li>
  <li>Internet Explorer 7</li>
  <li>Internet Explorer 8</li>
  <li>Firefox 3.5.5</li>
  <li>Safari 4.0.4</li>
  <li>Chrome 3.0</li>
  <li>Opera 10.10</li>
</ul>

<h2>Issues</h2>

There are number of issues existing, ofcourse, all related to Microsoft Internet Explorer:

<ul>
  <li>You have to always <b>preload fileUploader by calling fileUploader.load() during page load</b>. If you are using AJAX and instantiate first fileUploader.Uploader object during AJAX event, the uploader won't work. This is because of IE's security feature (i guess, or maybe another IE bug) which does not export ExternalInterface of Flash OBJECT to movie element when you inject OBJECT into DOM not during page load time.</li>
</ul>

More info to come...