Some JPEG operations can be lossless if you are using the right software (no picture quality is lost).  
This project aims to inform your choice.

| Platform | Software                                                                                          |  Rotate                                                                                                                               |   Crop   | Blur  | EXIF |
|----------|---------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------:|:-------------------:|
| Android  | **[Google Photos](https://play.google.com/store/apps/details?id=com.google.android.apps.photos)** | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/google-photos/pixel4/rotated_90degrees_four_times_comparison.jpg)            | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/google-photos/pixel4/cropped_comparison.jpg)         | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/google-photos/pixel4/privacy_comparison.jpg)         | ✅ Kept             |
| Android  | **[Samsung Gallery](https://play.google.com/store/apps/details?id=com.sec.android.gallery3d)**    | [✅ Lossless](https://github.com/lossless-jpg/data/blob/main/samsung-gallery/samsung_s10e/rotated_90degrees_four_times_comparison.jpg) | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/samsung-gallery/samsung_s10e/cropped_comparison.jpg) | [❌ Lossy](https://github.com/lossless-jpg/data/blob/main/samsung-gallery/samsung_s10e/privacy_comparison.jpg) | ✅ Kept             |
| Android  | **[PrivacyBlur](https://privacyblur.app)**                                                        | -                                                                                                                                      | -                                                                                                              | [❌ Lossy](https://github.com/MATHEMA-GmbH/privacyblur/issues/79)                                              | ❌ Lost             |
| Linux    | **[cropgui](https://github.com/jepler/cropgui)**                                                  | -                                                                                                                                      | ✅ Lossless                                                                                                    | -                                                                                                              | ✅ Kept            |
| UNIX/Win | **[jpegtran](https://jpegclub.org/jpegtran/)**                                                    | ✅ Lossless                                                                                                                            | ✅ Lossless                                                                                                    | -                                                                                                              | ✅ Not even updated |
| Web      | **[CropTool](https://croptool.toolforge.org)**                                                    | -                                                                                                                                      | ✅ Lossless                                                                                                    | -                                                                                                              | ✅ Kept             |

`-` means the software does not offer that feature.

# Operations

**Rotating** a JPEG should be lossless, as long as the length and height are a multiple of the block size (usually 16).

**Cropping** a JPEG should be lossless:
- if the crop does not remove the top-left corner of the image.
- or if the height removed from the top and width removed from the left are a multiple of the block size.
Ideal cropping tools let the user choose between lossless crop and lossy crop, with lossless crop snapping the cropping area to JPEG blocks.

**Blurring** (or drawing over a face/etc for privacy reasons) should only affect the blurred area and the blocks directly around it. The rest of the picture should be left intact.

# Help wanted

Please do not hesitate to add more software, add information, add operations!
To do so, please send a pull request or create an issue.
To add new software, please join 4 sample pictures as seen in the existing directories.
GUI software, command-line software, and even libraries are welcome.
Thanks a lot!

# Methodology

1. With the phone's default camera app, take a picture of a building with as few red areas as possible, and less than 50% of sky. Rename it to `original.jpg`.
2. If the app overwrites files, make a copy for each operation.
3. Rotate the picture by 90 degrees, save as `rotated_90degrees_four_times.jpg`, exit the app, then open `rotated_90degrees_four_times.jpg` and do it again. Doing it four times in total, the picture should be back into its original position.
4. Crop the bottom-right of the picture, so that only the top-left remains, save as `cropped.jpg`. Then on desktop use reliably lossless software to resize to a factor of 16 both that image and the original, so that the comparison works: `jpegtran -outfile cropped_jpegtran_cropped.jpg -copy all -crop 1600x1600+0+0 cropped.jpg`, `jpegtran -outfile original_jpegtran_cropped.jpg -copy all -crop 1600x1600+0+0 original.jpg`. Please note that jpegtran does not update EXIF thumbnails, which may induce some confusion.
5. Blur a tiny portion of the picture, save as `blurred.jpg`. If blurring is not available, use the pencil tool or anything that can hide a face.
6. Go to https://online-image-comparison.com (Highlight Color: Red, Fuzz: **0**) and compare each image to the original. Save all results with the `_comparison` suffix.

# Should I care?

## Quality

If you are taking a picture of your grandpa or baby, then the level of quality loss will probably not bother you.
On the other hand, if the picture is destined to have historical or encyclopedic value, then it is probably worth the effort trying to use lossless software. Future researchers zooming into a small detail of your picture will be thankful to have the real original pixels.

## File size

[JPEG tools have no idea what level of quality your picture has](https://photo.stackexchange.com/a/88186/1498). So when saving they use a default quality, or sometimes let you choose using a slider. All outcomes are regrettable:
- Choose a higher quality than needed: you get an unnecessarily bigger file size.
- Choose a lower quality than needed: you get artefacts visible to the naked eye, the picture looks more "pixelated" and has wrong colors.
- Even if you choose a similar quality setting, different software have different algorithms, so you will probably end up with a bigger file of lower quality.
