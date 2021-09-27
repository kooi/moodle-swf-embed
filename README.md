# Embed SWF in moodle

Workaround for using flash files (sfw) in a moodle course. A client-side javascript library is used to load embed the resource in a moodle _Page_. Embedded video is not supported; flash video files should be converted to a supported format (such as mp4).

## Requirements
 - [swf.js](https://github.com/swf2js/swf2js) This library (partially) supports Flash applets (technically this free version supports ActionScript 2.0; more details [swf2js.com](https://swf2js.com/en/)).

## Procedure
 1. Upload the `swf2js.js` file to your moodle course. Currently `swf2js` is not hosted at a CDN and improper mimetypes results in Cross-Origin Read Blocking (CORB) in the browser. More info at the [chromium project](https://www.chromium.org/Home/chromium-security/corb-for-developers). The file itself can be set to be invisible to students.
 2. Note down the moodle resource URL. This will be in the following form: `https://<moodleSite>/pluginfile.php/<contextId>/mod_resource/content/<itemId>/swf2js.js`
 3. Upload the `swf` file to your moodle course. As with the javascript library this can be set invisible for students.
 4. Note down the moodle resource URL. Again this will take the following form: `https://<moodleSite>/pluginfile.php/<contextId>/mod_resource/content/<itemId>/<filename>.swf`
 5. Create a _Page_.
 6. Edit the HTML of the page content (toolbar toggle -> Edit HTML source).
 7. Copy the contents of `embed.html` into the HTML source.
 8. Replace the `replace_with_moodle_url_for_swf2js.js` (line 1) with the URL to the swf2js-file.
 9. Replace the `replace_with_moodle_url_for_swf_file` (line 6) with the URL to the swf-file; 

## Source

```html
<script src="replace_with_moodle_url_for_swf2js.js"
        type="text/javascript"></script>
<script type="text/javascript">
    window.onload = () => {
        swf2js.load(
            'replace_with_moodle_url_for_swf_file',
            {
                "tagId": "player"
            }
        )
    }
</script>
<div id="player" style="height: 100pc; max-height: 900px;"></div>
```