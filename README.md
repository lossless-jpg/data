Some JPEG operations can be lossless if you are using the right software (no picture quality is lost).  
This project aims to inform your choice of software.

| Platform    | Software                                                                                          |  Rotate                                                                                                                                        |  Crop                                                                                                                 |  Blur                                                                                                                  |  EXIF               | Open source |
|-------------|---------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------------------------------------------------:|:-------------------:|:-----------:|
| Android     | **[Google Photos](https://play.google.com/store/apps/details?id=com.google.android.apps.photos)** | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/samples/google-photos/pixel4/rotated_90degrees_four_times_comparison.jpg)            | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/samples/google-photos/pixel4/cropped_comparison.jpg)         | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/samples/google-photos/pixel4/privacy_comparison.jpg)         | ✅ Kept             | ❌          |
| Android     | **[Samsung Gallery](https://play.google.com/store/apps/details?id=com.sec.android.gallery3d)**    | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samples/samsung-gallery/samsung_s10e/rotated_90degrees_four_times_comparison.jpg) | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/samples/samsung-gallery/samsung_s10e/cropped_comparison.jpg) | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/samples/samsung-gallery/samsung_s10e/privacy_comparison.jpg) | ✅ Kept             | ❌          |
| Android     | **[JPEG Cropper](https://play.google.com/store/apps/details?id=jp.kame.jpegcropper)**             | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samples/JPEG-Cropper/rotated_90degrees_four_times_comparison.jpg)                 | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samples/JPEG-Cropper/cropped_comparison.jpg)              | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samples/JPEG-Cropper/blurred_comparison.jpg)              | ✅ Kept             | ❌          |
| Android     | **[LLCrop](https://f-droid.org/packages/de.k3b.android.lossless_jpg_crop/)**                      | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samples/LLCrop/rotated_90degrees_four_times_comparison.jpg)                       | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samples/LLCrop/cropped_comparison.jpg)                    | [-](https://github.com/k3b/LosslessJpgCrop/issues/33)                                                                  | ✅ Kept             | ✅          |
| Android     | **[AJT](https://play.google.com/store/apps/details?id=jp.kame.ajt)**                              | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samples/AJT/rotated_90degrees_four_times_comparison.jpg)                          | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samples/AJT/cropped_comparison.jpg)                       | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samples/AJT/blurred_comparison.jpg)                       | ✅ Kept             | ❌          |
| Android     | **[ajpegtran](https://github.com/kamemak/ajpegtran_example/tree/pixelization_extension)**         | ✅ Lossless                                                                                                                                    | ✅ Lossless                                                                                                            | ✅ Lossless                                                                                                            | ✅ Kept             | ✅          |
| Android/iOS | **[PrivacyBlur](https://privacyblur.app)**                                                        | -                                                                                                                                              | -                                                                                                                      | [❌ Lossy](https://github.com/MATHEMA-GmbH/privacyblur/issues/79)                                                      | ❌ Lost             | ✅          |
| Linux       | **[cropgui](https://github.com/jepler/cropgui)**                                                  | -                                                                                                                                              | ✅ Lossless                                                                                                            | -                                                                                                                      | ✅ Kept             | ✅          |
| UNIX/Win    | **[jpegtran](https://jpegclub.org/jpegtran/)**                                                    | ✅ Lossless                                                                                                                                    | ✅ Lossless                                                                                                            | -                                                                                                                      | ✅ Kept             | ✅          |
| Windows     | **[Jpegcoll](https://sites.google.com/view/jpegcoll/home_en)**                                    | ✅ Lossless?                                                                                                                                   | ✅ Lossless?                                                                                                           | ✅ Lossless?                                                                                                           | ✅ Kept?            | ❌          |
| Windows     | **[Better JPEG](https://www.betterjpeg.com)**                                                     | ✅ Lossless?                                                                                                                                   | ✅ Lossless?                                                                                                           | ✅ Lossless?                                                                                                           | ✅ Kept?            | ❌          |
| Web         | **[CropTool](https://croptool.toolforge.org)**                                                    | -                                                                                                                                              | ✅ Lossless                                                                                                            | -                                                                                                                      | ✅ Kept             | ✅          |

`-` means the software does not offer that feature.  
`?` means not certified yet using the methodology below (testers welcome).

# Operations

**Rotating** a JPEG must be lossless, as long as the length and height are a multiple of the block size (usually 16).

**Cropping** a JPEG must be lossless if the crop does not remove the top-left corner of the image, or if the height removed from the top and width removed from the left are a multiple of the block size.
Ideal cropping tools let the user choose between lossless crop and lossy crop, with lossless crop snapping the crop area to JPEG blocks.

**Blurring** (or drawing over a face/etc for privacy reasons) should only affect the blurred area and the blocks directly around it. The rest of the picture must be left intact.

## Example of unwanted loss when blurring

I blurred passer-bys in the same politician picture using [Google Photos](https://play.google.com/store/apps/details?id=com.google.android.apps.photos) and [JPEG Cropper](https://play.google.com/store/apps/details?id=jp.kame.jpegcropper). then compared with the original. Here is how each tool performed:

| App | Blurred picture | Difference with original |
|---|---|---|
| Google Photos | ![pic](https://github.com/lossless-jpg/data/blob/main/samples/example/politician_google_photos.jpg?raw=true) | ![pic](https://github.com/lossless-jpg/data/blob/main/samples/example/politician_google_photos_comparison.jpg?raw=true) |
| JPEG Cropper | ![pic](https://github.com/lossless-jpg/data/blob/main/samples/example/politician_jpeg_cropper.jpg?raw=true) | ![pic](https://github.com/lossless-jpg/data/blob/main/samples/example/politician_jpeg_cropper_comparison.jpg?raw=true) |

As you can see, Google Photos unfortunately modified most of the picture, whereas JPEG Cropper only modified the blurred part, which is ideal.

# Should I care?

## Quality

If you are taking a picture of your grandpa or baby, then a tiny bit of quality loss will probably not bother you.
On the other hand, if the picture is destined to have historical or encyclopedic value, then it is probably worth the effort trying to use lossless software. Next-century researchers analyzing a tiny detail of your picture (like the politician in the example above) might be thankful to have the real original pixels.

## File size

[JPEG tools have no idea what level of quality your picture has](https://photo.stackexchange.com/a/88186/1498). So when saving the file, they use an arbitrary quality, or sometimes let you choose using a slider. All outcomes are regrettable:
- Choose a higher quality than needed: you get an unnecessarily bigger file size.
- Choose a lower quality than needed: you get artefacts visible to the naked eye, the picture looks more "pixelated" and has wrong colors.
- Even if you choose a similar quality setting, different tools have different algorithms, so you will probably end up with a bigger file of lower quality.

Using lossless software elegantly solves these problems, keeping the same file size with no quality loss.

# Help wanted

Please do not hesitate to add more software, add information, add operations!
To do so, please send a pull request or create an issue.
To add new software, please join 4 sample pictures as seen in the existing directories.
Mobile apps, desktop software, command-line software, and even libraries are welcome.
Thanks a lot!

# Methodology

1. With the phone's default camera app, take a picture of a building with as few red areas as possible, and less than 50% of sky. Rename it to `original.jpg`.
2. If the app overwrites files, make a copy for each operation.
3. Rotate the picture by 90 degrees, save as `rotated_90degrees_four_times.jpg`, exit the app, then open `rotated_90degrees_four_times.jpg` and do it again. Doing it four times in total, the picture should be back into its original position.
4. Crop the original picture so that only the top-left part remains, save as `cropped.jpg`. Then on desktop use reliably lossless software to crop both that image and the original to a size which is a factor of 16 (such as 1600x1600), so that they can be compared. Example: `jpegtran -outfile cropped_jpegtran_cropped.jpg -copy all -crop 1600x1600+0+0 cropped.jpg`, `jpegtran -outfile original_jpegtran_cropped.jpg -copy all -crop 1600x1600+0+0 original.jpg`. Please note that jpegtran does not update EXIF thumbnails.
5. Blur a tiny portion of the picture, save as `blurred.jpg`. If blurring is not available, use the pencil tool or anything that can hide a face.
6. Go to https://online-image-comparison.com (Highlight Color: Red, Fuzz: **0**) and compare each image to the original. Save all results with the `_comparison` suffix.
