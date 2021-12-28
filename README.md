Some JPEG operations can be lossless if you are using the right software. This project aims to inform your choice.

| Platform | Software                                                                                      |  Rotate  |   Crop   | Blur  | EXIF |
|----------|-----------------------------------------------------------------------------------------------|:--------:|:--------:|:-----:|:----:|
| Android  | [Google Photos](https://play.google.com/store/apps/details?id=com.google.android.apps.photos) | Lossy    | ?        | ?     | ?    |
| Android  | [Samsung Gallery](https://play.google.com/store/apps/details?id=com.sec.android.gallery3d)    | ?        | ?        | ?     | Kept |
| Android  | [PrivacyBlur](https://privacyblur.app)                                                        | -        | ?        | Lossy | Lost |
| Linux    | [cropgui](https://github.com/jepler/cropgui)                                                  | -        | Lossless | -     | Kept |
| UNIX/Win | [jpegtran](https://jpegclub.org/jpegtran/)                                                    | Lossless | Lossless | -     | ?    |
| Web      | [CropTool](https://croptool.toolforge.org)                                                    | -        | Lossless | -     | Kept |

`-` means the software does not offer that feature.

# Operations

Rotating a JPEG should be lossless, as long as the length and height are a multiple of the block size.

Cropping a JPEG should be lossless:
- if the crop affects only the bottom or right side of the image.
- or if the height taken from the top and width taken from the left are a multiple of the block size.
A good cropping tool should let the user choose between lossless crop and lossy crop, with lossless crop snapping the cropping area to blocks.

Blurring (or drawing over a face/etc for privacy reasons) should only affect the blurred area and the blocks directly around it. The rest of the picture should be left intact.

# Help wanted

Please do not hesitate to add more software, add information, add operations!
To do so, please send a pull request or create an issue.
To add new software, please join 4 sample pictures as seen in the existing directories.
GUI software, command-line software, and even libraries are welcome.
Thanks a lot!

# Methodology

1. With the phone's default camera app, take a picture of a building with as few red areas as possible, and less than 50% of sky.
2. If the app overwrites files, make a copy for each operation.
3. Rotate the picture by 90 degrees, save, exit the app. Do it four times.
4. Crop the bottom-right of the picture (then resize the image to the same as the original so that the comparison works, in GIMP Image>Canvas Size).
5. Blur a tiny portion of the picture.
6. Go to https://online-image-comparison.com (Highlight Color: Red, Fuzz: 1) and compare each image to the original. If there is any loss, save the result.
