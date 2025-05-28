# Full Screen Effects Addon for Godot 4

This Full Screen Effects addon is created specifically for 3D projects. It includes a variety of full-screen effects, supports multiple instances for each effect, and features a smooth fade system for seamless transitions. An example project is included to help you get up and running quickly.

Please note: this addon is provided as-is. While there won't be official support, I will be updating and fixing it as I continue work on my own project.

![Alt text](./preview.gif)

## Features

- **Full Screen Effects:**
  - Radial Blur
  - Screen Blur
  - FOV Shake
  - FOV Fade
  - Screen Shake
  - Fade from/to Color
  - Motion Blur
- **Multiple Instances:** 
  Multiple instances of each effect can be added and controlled individually.
- **Effect Management:**
  Built-in system to handle the fade-in, fade-out, and duration of each effect.
- **Example Project:**
  Includes a sample project demonstrating the usage of the addon.

## Installation

The installation process follows the standard procedure for any Godot addon:

1. Download the latest version of the addon.
2. Extract the addon and copy the `addons/ScreenEffects` folder into the root directory of your Godot project.
3. Navigate to **Project > Project Settings > Plugins**. Locate the "Full Screen Effects" plugin and set it to **Active**.
The addon should now be available for use in your project.

## Usage

The addon provides an easy-to-use API to add and manage full-screen effects. Here's an example using the **Radial Blur** effect.

### Example: Adding a Radial Blur Effect

To add a radial blur effect instance, use the following function call:

```gdscript
# Adds a single instance of Radial Blur effect with an amount of 1.25, 
# fade-in of 1.0 second, duration of 1.0 second, 
# and fade-out of 3.0 seconds.

ScreenEffects.AddRadialBlur(1.25, 1.0, 1.0, 3.0)
```

### Manipulating Effect Instances

You can store the ID of an effect instance to manipulate it later. If the duration is set to -1, the effect will continue indefinitely until manually stopped.

```gdscript
var mlRadialBlurInstanceID: int = -1

###################################################
# Add a Radial Blur effect with no fade-out (runs indefinitely).
if mlRadialBlurInstanceID == -1:
    mlRadialBlurInstanceID = ScreenEffects.AddRadialBlur(1.25, 1.0, -1.0, 3.0)

####################################################
# Update the amount of the Radial Blur effect to 0.5.
if mlRadialBlurInstanceID != -1:
    ScreenEffects.SetRadialBlurAmount(mlRadialBlurInstanceID, 0.5)

#####################################################
# Stop the Radial Blur effect and reset the ID.
if mlRadialBlurInstanceID != -1:
    ScreenEffects.StopRadialBlur(mlRadialBlurInstanceID)
    mlRadialBlurInstanceID = -1

```

## API Reference
The `EffectsHandler` class provides an interface for managing screen effects in Godot 4.x 3D projects. Below are the public methods for adding, configuring, and stopping effects like FOV fades, screen shakes, blurs, and color fades, as well as accessing viewport-related nodes.

### Methods

#### `GetPostProcessEffectsChainControl() -> Control`
Returns the `Control` node managing the post-process effects chain.  

#### `GetPostProcessViewportContainer() -> SubViewportContainer`
Returns the `SubViewportContainer` node used for post-processing.  
**Returns**: `null` if the container is invalid.

#### `GetPostProcessViewport() -> SubViewport`
Returns the `SubViewport` node within the post-process container.  
**Returns**: `null` if the container or viewport is invalid.

#### `AddFovFade(afFovMultiplier: float = 1.0, afFadeIn: float = 0.1, afDuration: float = 0.1, afFadeOut: float = 0.8) -> int`
Adds a field-of-view (FOV) fade effect.  
**Parameters**:  
- `afFovMultiplier`: Scales the camera’s FOV (default: `1.0`).  
- `afFadeIn`: Duration (seconds) to fade in (default: `0.1`).  
- `afDuration`: Duration (seconds) at full strength (default: `0.1`).  
- `afFadeOut`: Duration (seconds) to fade out (default: `0.8`).  
**Returns**: Unique ID of the effect instance, or `-1` if creation fails.  

#### `GetFovFadeInstanceById(alID: int) -> cFovFade`
Retrieves a FOV fade instance by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
**Returns**: The `cFovFade` instance, or `null` if not found.  

#### `StopFovFade(alID: int) -> void`
Stops a FOV fade effect by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  

#### `SetFovFadeMultiplier(alID: int, afX: float) -> void`
Updates the FOV multiplier for a FOV fade effect.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
- `afX`: New FOV multiplier value.  

#### `AddScreenShake(afForce: float = 0.1, afRate: float = 50.0, afFadeIn: float = 0.1, afDuration: float = 0.1, afFadeOut: float = 0.8) -> int`
Adds a screen shake effect.  
**Parameters**:  
- `afForce`: Shake amplitude (default: `0.1`).  
- `afRate`: Shake frequency (default: `50.0`).  
- `afFadeIn`: Duration (seconds) to fade in (default: `0.1`).  
- `afDuration`: Duration (seconds) at full strength (default: `0.1`).  
- `afFadeOut`: Duration (seconds) to fade out (default: `0.8`).  
**Returns**: Unique ID of the effect instance, or `-1` if creation fails.  

#### `GetScreenShakeInstanceById(alID: int) -> cScreenShake`
Retrieves a screen shake instance by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
**Returns**: The `cScreenShake` instance, or `null` if not found.  

#### `StopScreenShake(alID: int) -> void`
Stops a screen shake effect by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  

#### `SetScreenShakeForce(alID: int, afX: float) -> void`
Updates the force (amplitude) of a screen shake effect.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
- `afX`: New force value.  

#### `AddFovShake(afForce: float = 0.1, afRate: float = 50.0, afFadeIn: float = 0.1, afDuration: float = 0.1, afFadeOut: float = 0.8) -> int`
Adds a FOV shake effect.  
**Parameters**:  
- `afForce`: Shake amplitude (default: `0.1`).  
- `afRate`: Shake frequency (default: `50.0`).  
- `afFadeIn`: Duration (seconds) to fade in (default: `0.1`).  
- `afDuration`: Duration (seconds) at full strength (default: `0.1`).  
- `afFadeOut`: Duration (seconds) to fade out (default: `0.8`).  
**Returns**: Unique ID of the effect instance, or `-1` if creation fails.  

#### `GetFovShakeInstanceById(alID: int) -> cFovShake`
Retrieves a FOV shake instance by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
**Returns**: The `cFovShake` instance, or `null` if not found.  

#### `StopFovShake(alID: int) -> void`
Stops a FOV shake effect by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  

#### `SetFovShakeForce(alID: int, afX: float) -> void`
Updates the force (amplitude) of a FOV shake effect.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
- `afX`: New force value.  

#### `AddRadialBlur(afAmount: float = 1.0, afFadeIn: float = 0.1, afDuration: float = 0.1, afFadeOut: float = 0.8, avFocusPosition: Vector2 = Vector2(0.5, 0.5)) -> int`
Adds a radial blur effect.  
**Parameters**:  
- `afAmount`: Blur intensity (default: `1.0`).  
- `afFadeIn`: Duration (seconds) to fade in (default: `0.1`).  
- `afDuration`: Duration (seconds) at full strength (default: `0.1`).  
- `afFadeOut`: Duration (seconds) to fade out (default: `0.8`).  
- `avFocusPosition`: Center of the blur (default: `Vector2(0.5, 0.5)`).  
**Returns**: Unique ID of the effect instance, or `-1` if creation fails.  

#### `GetRadialBlurInstanceById(alID: int) -> cRadialBlur`
Retrieves a radial blur instance by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
**Returns**: The `cRadialBlur` instance, or `null` if not found.  

#### `SetRadialBlurFocusPosition(alID: int, avPosition: Vector2) -> void`
Updates the focus position of a radial blur effect.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
- `avPosition`: New focus position (`Vector2`).  
**Note**: Currently sets the property instantly.

#### `StopRadialBlur(alID: int) -> void`
Stops a radial blur effect by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  

#### `AddScreenBlur(afAmount: float = 1.0, afFadeIn: float = 0.1, afDuration: float = 0.1, afFadeOut: float = 0.8) -> int`
Adds a uniform screen blur effect.  
**Parameters**:  
- `afAmount`: Blur intensity (default: `1.0`).  
- `afFadeIn`: Duration (seconds) to fade in (default: `0.1`).  
- `afDuration`: Duration (seconds) at full strength (default: `0.1`).  
- `afFadeOut`: Duration (seconds) to fade out (default: `0.8`).  
**Returns**: Unique ID of the effect instance, or `-1` if creation fails.  

#### `GetScreenBlurInstanceById(alID: int) -> cScreenBlur`
Retrieves a screen blur instance by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
**Returns**: The `cScreenBlur` instance, or `null` if not found.  

#### `SetScreenBlurAmount(alID: int, afAmount: float) -> void`
Updates the blur intensity of a screen blur effect.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
- `afAmount`: New blur intensity.  

#### `StopScreenBlur(alID: int) -> void`
Stops a screen blur effect by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  

#### `SetMotionBlurActive(abX: bool) -> void`
Enables or disables motion blur globally.  
**Parameters**:  
- `abX`: `true` to enable, `false` to disable.  

#### `GetMotionBlurActive() -> bool`
Checks if motion blur is active.  
**Returns**: `true` if enabled, `false` otherwise.  

#### `AddScreenFade(afFadeDuration: float = 1.0, aStartColor: Color = Color(0,0,0,1), aEndColor: Color = Color(0,0,0,0)) -> int`
Adds a screen fade effect transitioning between two colors.  
**Parameters**:  
- `afFadeDuration`: Total duration (seconds) of the fade (default: `1.0`).  
- `aStartColor`: Starting color (default: opaque black).  
- `aEndColor`: Ending color (default: transparent).  
**Returns**: Unique ID of the effect instance, or `-1` if creation fails.  

#### `GetScreenFadeInstanceById(alID: int) -> cScreenFade`
Retrieves a screen fade instance by its ID.  
**Parameters**:  
- `alID`: The ID of the effect instance.  
**Returns**: The `cScreenFade` instance, or `null` if not found.  

#### `SetCamera(aCamera: Camera3D) -> void`
Sets the camera used for rendering effects.  
**Parameters**:  
- `aCamera`: The `Camera3D` node to use.  

## Roadmap
No future updates planned currently. 

## Example Project
An example project demonstrating the usage of this addon is included in the repository. Check the example_project/ folder for a working setup that shows how to integrate and manage the effects in your own project.

## License
This addon is licensed under the MIT License. See the LICENSE file for more information.
