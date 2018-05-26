# Audit of the Bootstrap project
In this documenation you'll find the result of performance techniques that are applied to the Bootstrap project. Each section will have an audit that is taken before and after applying the technique.

## Images
The Bootstrap project consist of a couple images that have a file size around ~170 kb.

![Overview of the images that are loaded](audit-assets/images-before.PNG)

What we can do to increase performance is compressing the images. For this test, [compressjpgeg](http://compressjpeg.com/nl/) is used. Compressjpeg is a site where you're able to upload your files to the site and they compressed the images for you. After that you're able to download all of the files that you've uploaded.

![Compression of images](audit-assets/images-compression.PNG)

The photo below is the audit after compressioning the images. As you can see the average size of the images are: ~80kb. That is a decrease of ~55%. 

![Overview of the images that are loaded after compression](audit-assets/images-after.PNG)


### Conclusion

By compressioning the images you're able to decrease the overall size by ~55%. This is really big for mobile users that have limited data plan. However compressing images by uploading to Compressjpeg takes a lot of time. I suggest using an automatic tool like [compress-images](https://www.npmjs.com/package/compress-images) or else use this tool only if the overal size of the project is getting out of hand.


