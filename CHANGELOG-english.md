# Changelog

## 2024-03-25

- v24.3.3
- Fixed ImportError for the create_binary_mask function in versions below webui 1.6.0

## 2024-03-21

- v24.3.2
- Fixed opencv error when inputting image_mask without going through UI
- When enabling skip img2img option in img2img inpaint, adetailer is disabled
  - There is a hard-to-solve issue regarding the size of the mask

## 2024-03-16

- v24.3.1
- Updated ultralytics to support YOLO World v2, YOLO9 versions
- Changed to operate in inpaint mode when inpaint full res
- When not inpaint full res, only select masks that intersect with the mask entered by the user

## March 1, 2024

- v24.3.0
- Added YOLO World model: Only the largest yolov8x-world.pt model is selectable by default.
- Enabled use of ControlNet from lllyasviel/stable-diffusion-webui-forge (PR #517)
- Added soft_inpainting to the default script list (https://github.com/AUTOMATIC1111/stable-diffusion-webui/pull/14208)
  - Not retroactively applicable to those who have previously installed

- Added simple pytest for detection models
- Added `Passthrough` option to xyz grid ControlNet model options

## January 23, 2024

- v24.1.2
- Added `Passthrough` option to controlnet model. Uses the controlnet options entered as inputs
- Added fastapi endpoints

## January 10, 2024

- v24.1.1
- SDNext compatibility update (issue #466)
  - Added default values to configuration state
  - Modified to change the state whenever widget values are changed (previously applied when the create button was pressed)
- Made the `inpaint_depth_hand` ControlNet model recognized as a depth model (issue #463)

## January 4, 2024

- v24.1.0
- Added `depth_hand_refiner` ControlNet (PR #460)

## December 30, 2023

- v23.12.0
- Changed the method of copying script_args to avoid errors due to deepcopy for several scripts that add files as arguments
- Improved the skip img2img process by fixing the width and height to 128
- Automatically disabled adetailer in img2img inpainting mode
- Changed to always keep the first created params.txt file

## November 19, 2023

- v23.11.1
- Added negpip to the default script list
  - Not retroactively applicable to those who have previously installed
- Fixed an issue where the skip img2img option was not applied correctly when more than 2 steps
- Fixed an issue where images were entered as np.ndarray in SD.Next
- Added controlnet path to sys.path so that no import errors occur even when specifying --data-dir.

## October 30, 2023

- v23.11.0
- Changed image index calculation method
  - Made running adetailer impossible under webui versions lower than 1.1.0
- Increased choices for controlnet preprocessor
- Added an option to set an additional yolo model directory
- Fixed an issue where items with `/` in infotext were not restored from exif
  - Images created in previous versions still not restored
- Added an option to always apply the same seed in the same tab
- Displayed a message that ControlNet version 1.1.411 (f2aafcf2beb99a03cbdf7db73852228ccd6bd1d6) cannot be used under webui versions lower than 1.6.0

## October 15, 2023

- v23.10.1
- Added prompt S/R to xyz grid
- Modified to change sampler names as well when processing sampler for samples with steps == 1 in img2img

## October 7, 2023

- v23.10.0
- No longer continuously attempts to download when failing to download Huggingface models
- Added a feature to skip the img2img stage in img2img
- Showed the detection stage in live preview (PR #352)

## September 20, 2023

- v23.9.3
- Updated to ultralytics version 8.0.181 (https://github.com/ultralytics/ultralytics/pull/4891)
- Lazily imported mediapipe and ultralytics

## September 10, 2023

- v23.9.2
- (Experimental) Added VAE selection feature

## September 1, 2023

- v23.9.1
- Fixed backward compatibility issues caused by additional arguments in webui 1.6.0

## August 31, 2023

- v23.9.0
- (Experimental) Added checkpoint selection feature
  - Refresh button omitted from implementation due to bugs
- With the 1.6.0 update, no longer switched to Euler when an unavailable sampler was selected in img2img
- Instead of causing an error when an invalid argument was passed, disabled adetailer

## August 25, 2023

- v23.8.1
- Fixed an issue where adetailer gets disabled after setting the model to `None` in the xyz grid
- Stops the process when skip is pressed
- Allows CPU usage even when `--medvram-sdxl` is set

## August 14, 2023

- v23.8.0
- Added `[PROMPT]` keyword. Used in `ad_prompt` or `ad_negative_prompt` to replace it with the input prompt (PR #243)
- Added Only the top k largest option (PR #264)
- Updated the ultralytics version

## July 31, 2023

- v23.7.11
- Added separate clip skip option
- Cleaned up install requirements (new version of ultralytics, mediapipe~=3.20)

## July 28, 2023

- v23.7.10
- Cleaned up import statements for ultralytics, mediapipe
- Removed color in traceback (because of API), set to display library versions
- Removed huggingface_hub, pydantic from install.py
- Deleted unused controlnet-related code

## July 23, 2023

- v23.7.9
- Resolved `ModuleNotFoundError` for `ultralytics.utils` (https://github.com/ultralytics/ultralytics/issues/3856)
- Set to not install versions above `pydantic` 2.0
- Fixed `controlnet_dir` cmd args issue (PR #107)

## July 20, 2023

- v23.7.8
- Reverted the addition of `paste_field_names`

## July 19, 2023

- v23.7.7
- Added an option to select a separate sampler during the inpainting phase (also added to the xyz grid)
- Fixed a batch index issue in versions below webui 1.0.0-pre
- Added `paste_field_names` to the script. Its use is uncertain

## July 16, 2023

- v23.7.6
- Pre-installed `py-cpuinfo` for the cpuinfo feature added in `ultralytics 8.0.135`. (Restart required if not pre-installed when using CPU or MPS)
- Changed init_image to RGB mode if not in RGB

## July 7, 2023

- v23.7.4
- Fixed an issue with the prompt index when batch count > 1

- v23.7.5
- Adjusted so that `cached_uc` and `cached_c` in i2i are different instances from those in p

## July 5, 2023

- v23.7.3
- Bug fixes
  - Issue with `object()` not being JSON serializable
  - Fixed a problem where all_prompts became fixed when batch count was greater than 2 due to calling `process`
  - The filenames for `ad-before` and `ad-preview` images were different from the actual filenames
  - Compatibility issue with pydantic 2.0

## July 4, 2023

- v23.7.2
- Added `mediapipe_face_mesh_eyes_only` model: uses only eyes detected by `mediapipe_face_mesh`
- Calls `scripts.postprocess` before each batch and `scripts.process` after
  - Using controlnet slightly increases the time taken but helps solve some issues
- Added `lora_block_weight` to the script whitelist
  - Those who have used ADetailer at least once need to manually add it

## July 3, 2023

- v23.7.1
- Called `StableDiffusionProcessing` object close after `process_images`.
- Added attribute to check if it was used via API call
- Continued the rest of the process without stopping when a `NansException` occurs

## July 2, 2023

- v23.7.0
- If a `NansException` occurs, it logs it and returns the original image
- Used `rich` for error tracing
  - Added `rich` to install.py
- Fixed an issue where changing the value of a component during creation would also change the value in args (issue #180)
- Terminal log allows checking the actual prompt applied to ad_prompt and ad_negative_prompt (only if different from input)

## June 28, 2023

- v23.6.4
- Increased maximum model count from 5 to 10
- Added a note that if ad_prompt and ad_negative_prompt are left blank, the input prompt is used
- Logging for failure to download Huggingface models
- Fixed an issue where if the 1st model was `None`, the rest of the inputs were ignored
- When `--use-cpu` is set, YOLO models use the CPU

## June 20, 2023

- v23.6.3
- Enabled the use of three modules for ControlNet inpaint model
- Added Noise Multiplier option (PR #149)
- Set pydantic's minimum version to 1.10.8 (Issue #146)

## June 5, 2023

- v23.6.2
- Enabled the use of ADetailer in the xyz_grid.
  - Only applied to 8 options in the first tab.

## June 1, 2023

- v23.6.1
- Support for 5 ControlNet models: `inpaint, scribble, lineart, openpose, tile` (PR #107)
- Added start and end arguments for controlnet guidance (PR #107)
- Changed to use `modules.extensions` to load and find paths for ControlNet extensions
- Separated ControlNet into a different function in the UI

## May 30, 2023

- v23.6.0
- Changed the script name from `After Detailer` to `ADetailer`
  - API users need to update accordingly
- Several configuration changes:
  - `ad_conf` → `ad_confidence`. Changed from an int range of 0~100 to a float range of 0.0~1.0
  - `ad_inpaint_full_res` → `ad_inpaint_only_masked`
  - `ad_inpaint_full_res_padding` → `ad_inpaint_only_masked_padding`
- Added mediapipe face mesh model
  - Minimum version for mediapipe set to `0.10.0`
- Removed rich traceback
- Made it so errors don't occur and the model is removed when Huggingface downloads fail

## May 26, 2023

- v23.5.19
- Added a `None` option to the first tab
- Blocked the use of non-inpaint ControlNet models via API in ad controlnet model
- Stopped total tqdm progress bar updates during ADetailer process
- Stopped ADetailer process in the state.interrupted state
- Changed to call the ControlNet process only after each batch completes

### May 25, 2023

- v23.5.18
- ControlNet related adjustments:
  - Changed all units’ `input_mode` to `SIMPLE`
  - Added functionality to revert ControlNet unet hooks and hijack functions only during ADetailer execution
  - Resumed ControlNet script process after ADetailer processing is finished. (Solves issue with batch count 2 and above)
- Removed ControlNet from the default active script list

### May 22, 2023

- v23.5.17
- If there is a ControlNet extension, the ControlNet script is activated. (Solves related ControlNet issues)
- Set elem_id for all components
- Displayed version in UI

### Further entries detail adjustments to the tool, including the addition of new features, bug fixes, and enhancements to improve user interaction and system functionality.

## May 19, 2023

- v23.5.16
  - Added options:
    - Mask min/max ratio
    - Mask merge mode
    - Restore faces after ADetailer
  - Grouped options into an Accordion.

## May 18, 2023

- v23.5.15
  - Changed to only import what is necessary (fixed VAE loading error, and improved loading speed).

## May 17, 2023

- v23.5.14
  - Added functionality to skip parts of the ad prompt with `[SKIP]`.
  - Added bbox alignment option.
  - Created type hints for sd_webui.
  - Fixed an API error related to the enable checker?

## May 15, 2023

- v23.5.13
  - Added functionality to separate and apply the ad prompt with `[SEP]`.
  - Changed enable checker back to pydantic.
  - Separated UI related functions to the adetailer.ui folder.
  - Deactivated all ControlNet units when using ControlNet.
  - Created the adetailer folder if it does not exist.

## May 13, 2023

- v23.5.12
  - Changed inputs, excluding `ad_enable`, to come in dict type.
    - Especially easier to use via web API.
    - web API breaking change.
  - Fixed an error where `mask_preprocess` argument was not included (PR #47).
  - Added option to not download models from Huggingface `--ad-no-huggingface`.

## May 12, 2023

- v23.5.11
  - Removed `ultralytics` warning.
  - Removed unnecessary exif arguments further.
  - Added `use separate steps` option.
  - Adjusted the UI layout.

## May 9, 2023

- v23.5.10
  - Added option to apply ADetailer only to the selected scripts, default value `True`. Selectable in the settings tab.
    - Default: `dynamic_prompting,dynamic_thresholding,wildcards,wildcard_recursive`.
  - Added `person_yolov8s-seg.pt` model.
  - Set the minimum version for `ultralytics` to `8.0.97` (Addressed issue with C:\\).

## May 8, 2023

- v23.5.9
  - Enabled the use of more than two models. Default: 2, Maximum: 5.
  - Enabled the use of segment models. Added `person_yolov8n-seg.pt`.

## May 7, 2023

- v23.5.8
  - Support added for arrow keys in prompts and negative prompts (PR #24).
  - Added `mask_preprocess`. The seed value may differ from previous versions!
  - Stored the before image only if an image processing occurred.
  - Modified the settings label to be more appropriate than ADetailer.

## May 6, 2023

- v23.5.7
  - Added `ad_use_cfg_scale` option. Decides whether to use CFG scale separately.
  - Changed the `ad_enable` default value from `True` to `False`.
  - Changed the `ad_model` default value from `None` to the first model.
  - Operates with a minimum of 2 inputs (ad_enable, ad_model).

- v23.5.7.post0
  - Executed `init_controlnet_ext` only when controlnet_exists == True.
  - Displayed `ultralytics` warning for users who installed the webui directly under the C drive.

## May 5, 2023 (Children's Day)

- v23.5.5
  - Added `Save images before ADetailer` option.
  - Produced an error message if the length of the input arguments and ALL_ARGS differs.
  - Added installation methods to README.md.

- v23.5.6
  - Provided detailed error messages in case of IndexError in get_args.
  - Embedded extra_params in AdetailerArgs.
  - Deep copied scripts_args.
  - Slightly separated postprocess_image.

- v23.5.6.post0
  - Provided detailed error messages in `init_controlnet_ext`.

## May 4, 2023

- v23.5.4
  - Used pydantic for arguments validation.
  - Reverted: ad_model to `None` as default.
  - Reverted: `__future__` imports.
  - Lazily imported yolo and mediapipe.

## May 3, 2023

- v23.5.3.post0
  - Removed `__future__` imports.
  - Changed to copy scripts and scripts args.

- v23.5.3.post1
  - Changed default ad_model from `None`.

## May 2, 2023

- v23.5.3
  - Removed `None` from the model list and added `Enable ADetailer` checkbox.
  - Fixed `skip_install` in install.py.
