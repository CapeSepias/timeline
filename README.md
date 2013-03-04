Timeline
========

* Copyright (c) 2013 [The Wellcome Library](http://wellcomelibrary.org/)
* License: [MIT](http://en.wikipedia.org/wiki/MIT_License)
* Uses: [jQuery](https://github.com/jquery/jquery), [jQueryUI](https://github.com/jquery/jquery-ui), [moment](https://github.com/timrwood/moment), [iScroll](https://github.com/cubiq/iscroll), [jQuery Address](https://github.com/asual/jquery-address), [easyXDM](https://github.com/oyvindkinsey/easyXDM), [json2](https://github.com/douglascrockford/JSON-js)
* [Example Timeline](http://wellcomelibrary.org/using-the-library/subject-guides/genetics/makers-of-modern-genetics/genetics-timeline/)


## Embedding

You will notice that the [Example Timeline](http://wellcomelibrary.org/using-the-library/subject-guides/genetics/makers-of-modern-genetics/genetics-timeline/) has an 'embed' option in the bottom-left corner.

You can use the code in this panel to embed the timeline on your own website, e.g: 

	<div class="timeline" data-uri="/content/timelines/history-of-genetics-timeline/" data-eventid="" style="width:600px; height:600px; background-color: #000"></div>
	<script type="text/javascript" src="http://wellcomelibrary.org/plugins/timeline/embed.min.js"></script><script type="text/javascript">/* wordpress fix */</script>

The timeline also supports 'deep linking' to events, where a hash value is appended to the Url as you browse e.g: 

http://wellcomelibrary.org/using-the-library/subject-guides/genetics/makers-of-modern-genetics/genetics-timeline/#16121


##Developers 

The timeline project is split into `/src` and `/build` directories, with a [`build.ps1`](https://github.com/wellcomelibrary/timeline/blob/master/build.ps1) [PowerShell](http://en.wikipedia.org/wiki/Windows_PowerShell) script in the root of the project which combines and minifies the various JavaScript files into [`embed.min.js`](https://github.com/wellcomelibrary/timeline/blob/master/build/embed.min.js) and [`wellcomeTimeline.min.js`](https://github.com/wellcomelibrary/timeline/blob/master/build/wellcomeTimeline.min.js), (right click > Run with PowerShell).

* [`embed.min.js`](https://github.com/wellcomelibrary/timeline/blob/master/build/embed.min.js) - creates an iframe within `div.timeline` to host [`timeline.html`](https://github.com/wellcomelibrary/timeline/blob/master/src/timeline.html). 
* [`wellcomeTimeline.min.js`](https://github.com/wellcomelibrary/timeline/blob/master/build/wellcomeTimeline.min.js) - contains all the jQueryUI widgets used to create the user interface, plus a few utility scripts.


To get the project running on localhost, create a website pointing to the `/src` directory with a virtual directory called 'build' pointing to the `/build` directory.

Alternatively, move the minified scripts into the `/src` directory.

To debug individual scripts, open [`timeline.html`](https://github.com/wellcomelibrary/timeline/blob/master/src/timeline.html), comment out [`wellcomeTimeline.min.js`](https://github.com/wellcomelibrary/timeline/blob/master/build/wellcomeTimeline.min.js) and uncomment the scripts directly underneath.


### Data Format

The [example timeline data](http://wellcomelibrary.org/content/timelines/history-of-genetics-timeline/) employs the use of [Julian days](http://en.wikipedia.org/wiki/Julian_day). These are useful for plotting applications as they represent a calendar-independent, absolute unit of time.

However, the code controlling the main user interface only deals in [`moment`](https://github.com/timrwood/moment) objects.

The timeline loosely employs the [Provider Model](http://en.wikipedia.org/wiki/Provider_model), which abstracts the date parsing out to [`wellcomeTimelineProvider.js`](https://github.com/wellcomelibrary/timeline/blob/master/src/js/wellcomeTimelineProvider.js).

Providers could be created to work with any arbitrary date format that can be converted to [`moment`](https://github.com/timrwood/moment) objects.

To change the provider, edit the `provider` option of the `wellcomeTimeline` widget in [`timeline.html`](https://github.com/wellcomelibrary/timeline/blob/master/src/timeline.html).

Use the `data-uri` attribute of `div.timeline` to set the path to your custom data source.

### Notes

The `/* wordpress fix */` empty script in the embed code is for convenience when using the Wordpress WYSIWYG editor, which will otherwise strip out the script tags.


