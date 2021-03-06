# Audit of the Bootstrap project
In this documenation you'll find the result of performance techniques that are applied to the Bootstrap project. Each section will have an audit that is taken before and after applying the technique.

## Images
The Bootstrap project consist of a couple images that have a file size around ~170 kb.

*before*

![Overview of the images that are loaded](audit-assets/images-before.PNG)

What we can do to increase performance is compressing the images. For this test, [compressjpgeg](http://compressjpeg.com/nl/) is used. Compressjpeg is a site where you're able to upload your files to the site and they compressed the images for you. After that you're able to download all of the files that you've uploaded.

![Compression of images](audit-assets/images-compression.PNG)

The photo below is the audit after compressioning the images. As you can see the average size of the images are: ~80kb. That is a decrease of ~55%. 

*after*

![Overview of the images that are loaded after compression](audit-assets/images-after.PNG)


### Conclusion

By compressioning the images you're able to decrease the overall size by ~55%. This is really big for mobile users that have limited data plan. However compressing images by uploading to Compressjpeg takes a lot of time. I suggest using an automatic tool like [compress-images](https://www.npmjs.com/package/compress-images) or else use this tool only if the overal size of the project is getting out of hand.

## Custom font

Bootstrap loads two fonts, both have a file size around ~75kb.

*before*
![Overview of fonts loaded](audit-assets/font-before.PNG)

We can decrease the file by __subsetting__ the font.

>Regular Typotheque fonts support over 100 languages and advanced typographic features such as small caps, different numeral styles, alternative characters and special symbols. Web browsers, however, can access only a small fraction of those characters. Removing these inaccessible features makes the files much smaller, so they download much quicker. Users can specify which languages to support. - [Typotheque](https://www.typotheque.com/help/webfonts/what_is_font_subsetting)

The subsetting tool that used is: [FontSquirel](https://www.fontsquirrel.com/tools/webfont-generator). FontSquirel is a site where you can upload the font that you what to subset, and download the subset font when the process is done.

*after*

![Overview of fonts loaded after subsetting them](audit-assets/font-after.PNG)

As you can see from the after photo, the file size is now ~27kb. A decrease of ~66%. That is enormous. However FontSquirel only process the subset font to the WOFF and WOFF2 format. Either way you're able to rely on the CSS fallback, where you try the subset format and if that's not working, than load the normal font.

### Conclusion
Subsetting your font can be a good idea to decrease file size. Subsetting is a one time process where the outcome can give a lot of benefit, although you're only able to have a WOFF and WOFF2 format. I recommend to add this process to future projects.


## CSS

Bootstrap loads three CSS files on the homepage. To increase performance we can minify those file. 

>This minifier removes whitespace, strips comments, combines files, and optimizes/shortens a few common programming patterns.
And it comes with a huge test suite.  - [Minifier] (https://www.minifier.org/)

*before*

![Audit of CSS ](audit-assets/css-before.PNG)

The tool that is used to minify CSS is [Minifier](https://www.minifier.org/). With this tool you're able to upload your CSS file to their site. After the minify process, you're able to download the minified files and add this to your project.

![Audit of CSS after minifying ](audit-assets/css-after.PNG)

As you can see on the photo, the minified proces have a more pronounce impact on the really big file. The Bootstrap.css file (before) have a file size of 149kb and have had a decrease of ~21% procent after the minified process. 

### Conclusion
The steps taken to minify the CSS file was really easy and it have decreased the overal file size by ~21%. I recommend adding this process to your project by adding a automatic like [Uglifycss](https://www.npmjs.com/package/uglifycss) or use the tool that is used in this example before deploying.

### G-Zip

By performing a google audit, the audit gives us a suggestion of using G-Zip

![Google audit: sugesstion](audit-assets/g-zip-google-audit.PNG)

To add g-zip to our process, we're using the node module: [Compression](https://github.com/expressjs/compression). Compression is a Node.js Middleware.

To add compression to our project we need to install the module.

install dependencies
```
npm install --save compression
```

include in your main js file
```js
//require dependencie
const compression = require('compression');
const app = express();

app.use(compression({filter: shouldCompress}));

function shouldCompress (req, res) {
    if (req.headers['x-no-compression']) {
        // don't compress responses with this request header
        return false
    }
    console.log('test')

    // fallback to standard filter function
    return compression.filter(req, res)
}
```

To check our compression we're going to use:[Check Gzip Compression](https://checkgzipcompression.com/). 

![Result of using G-Zip](audit-assets/g-zip-checker.PNG)

According to this tool we've decrease our size by 72.1%. That's huge! Also using the compression was really simple.

### Conclusion
G-Zip can be a very usefull tool for compressing your whole project. The installation was very easy and the result was very amazing, a decrease in file size by 72.1%! I recommend using G-Zip compression in your project.