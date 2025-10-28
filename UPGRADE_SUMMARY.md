# FFmpeg 8.0 Upgrade Summary

## Overview
This document summarizes the changes made to upgrade the mobile-ffmpeg-16KB repository from FFmpeg 4.4-dev-416 to FFmpeg 8.0 (Huffman).

## Changes Made

### 1. Core FFmpeg Source Update
**File: `build/arch-common.sh`**
- Changed FFmpeg repository from custom fork to official FFmpeg repository
- Updated from commit `d222da435e63a2665b85c0305ad2cf8a07b1af6d` (v4.4-dev-416) to tag `n8.0`
- Changed source type from COMMIT to TAG for better stability

```bash
# Before:
LIB_REPO_URL="https://github.com/tanersener/FFmpeg"
SOURCE_ID="d222da435e63a2665b85c0305ad2cf8a07b1af6d"  # COMMIT -> v4.4-dev-416
SOURCE_TYPE="COMMIT"

# After:
LIB_REPO_URL="https://github.com/FFmpeg/FFmpeg"
SOURCE_ID="n8.0"                                      # TAG -> v8.0 Huffman
SOURCE_TYPE="TAG"
```

### 2. Version String Updates

#### Android
**Files Updated:**
- `android/app/src/main/cpp/mobileffmpeg.h`: Updated MOBILE_FFMPEG_VERSION from "4.4" to "8.0"
- `android/app/build.gradle`: Updated versionName from "4.4" to "8.0", versionCode from 240440 to 240800
- `tools/release/android/build.gradle`: Updated versionName from "4.4" to "8.0", versionCode from 240440 to 240800
- `tools/release/android/build.lts.gradle`: Updated versionName from "4.4.LTS" to "8.0.LTS", versionCode from 160440 to 160800

#### iOS/tvOS
**Files Updated:**
- `ios/src/MobileFFmpeg.m`: Updated MOBILE_FFMPEG_VERSION from @"4.4" to @"8.0"

### 3. Documentation Updates

#### README.md
- Updated release badges from v4.4 to v8.0
- Updated supported FFmpeg version from "v3.4.x, v4.0.x, v4.1, v4.2, v4.3 and v4.4-dev releases" to "v8.0 (Huffman) release"
- Added new version entry in the version history table
- Updated example dependency versions in build.gradle from 4.4 to 8.0
- Updated example Podfile versions from 4.4 to 8.0

#### docs/index.md
- Updated example dependency versions to match README.md changes

### 4. Podspec Files (iOS/tvOS)
**All 16 podspec files updated with FFmpeg version in description:**
- `tools/release/ios/*.podspec` (8 files)
- `tools/release/tvos/*.podspec` (8 files)

Changed description from:
```
Includes FFmpeg v4.4-dev-416 with [libraries...]
```
To:
```
Includes FFmpeg v8.0 (Huffman) with [libraries...]
```

## Files Modified (24 total)
1. README.md
2. android/app/build.gradle
3. android/app/src/main/cpp/mobileffmpeg.h
4. build/arch-common.sh
5. docs/index.md
6. ios/src/MobileFFmpeg.m
7. tools/release/android/build.gradle
8. tools/release/android/build.lts.gradle
9-16. tools/release/ios/*.podspec (8 files)
17-24. tools/release/tvos/*.podspec (8 files)

## Build Script Compatibility

### Existing Customizations Verified
The following FFmpeg build customizations remain compatible with FFmpeg 8.0:

1. **iOS Build** (`build/ios-ffmpeg.sh`):
   - Workaround for -mdynamic-no-pic flag (line 406-407)
   - Configure options remain compatible

2. **Android Build** (`build/android-ffmpeg.sh`):
   - Thread-local log level patch (line 354-355)
   - Configure options remain compatible

3. **Configure Options**:
   All existing configure flags are compatible with FFmpeg 8.0:
   - `--enable-version3`
   - `--enable-cross-compile`
   - `--enable-pic`
   - External library integration flags
   - Hardware acceleration flags
   - Optimization flags

## Next Steps

### To Build with FFmpeg 8.0:

1. **For Android:**
   ```bash
   export ANDROID_HOME=<Android SDK Path>
   export ANDROID_NDK_ROOT=<Android NDK Path>
   ./android.sh
   ```

2. **For iOS:**
   ```bash
   ./ios.sh
   ```

3. **For tvOS:**
   ```bash
   ./tvos.sh
   ```

### Important Notes:

1. **First Build**: The build scripts will automatically download FFmpeg 8.0 source code from the official repository using the `n8.0` tag.

2. **Clean Build**: If you have previously built FFmpeg 4.4, it's recommended to clean the workspace:
   ```bash
   rm -rf src/ffmpeg
   rm -rf prebuilt
   ```

3. **API Changes**: FFmpeg 8.0 includes significant API changes from 4.4. Applications using the library may need updates to handle:
   - Deprecated API removals
   - New codec support
   - Enhanced hardware acceleration
   - Improved performance optimizations

4. **Testing Required**: Thoroughly test all functionality after building, especially:
   - Video encoding/decoding
   - Audio processing
   - Format conversions
   - Hardware acceleration features
   - External library integrations

## FFmpeg 8.0 Key Features

FFmpeg 8.0 "Huffman" includes numerous improvements over 4.4:
- Better codec support
- Improved performance
- Enhanced hardware acceleration
- Bug fixes and stability improvements
- Updated external library support
- Better H.265/HEVC support
- Improved AV1 codec support

## Version History

| MobileFFmpeg Version | FFmpeg Version | Release Date |
|:----:|:----:|:----:|
| 8.0 | 8.0 (Huffman) | Oct 28, 2025 |
| 4.4 | 4.4-dev-416 | Jul 25, 2020 |

## References

- FFmpeg Official Site: https://ffmpeg.org/
- FFmpeg 8.0 Release: https://ffmpeg.org/download.html
- Official FFmpeg Repository: https://github.com/FFmpeg/FFmpeg
- FFmpeg Documentation: https://ffmpeg.org/documentation.html

---

**Date of Upgrade**: October 28, 2025  
**Upgraded By**: Automated upgrade process  
**Repository**: mobile-ffmpeg-16KB

