# Progress Bar System

A customizable progress bar system for Godot 4 with visual effects, animations, and multiple display modes.

## Features

  * Multiple bar styles: Solid, RGB, Health Bar, Rainbow Wave, Fluid
  * Fill modes: Discrete segments, Fade transitions, Pour animation  
  * Visual effects: Wave, Bubbles, Glitch, Static, Pixel Static
  * Flash effects: Segment flash, drain effects, multi-segment flash
  * Custom frames: Support for custom frame textures
  * Smooth transitions: Animated value changes with configurable speed

## Quick Setup

1. Create a ColorRect node in your scene
2. Apply the "progress_bar.gdshader" to the ColorRect material
3. Attach the "progress_bar.gd" script to the ColorRect
4. Configure the bar in the inspector or through code

## Basic Usage

# Set up the bar
progress_bar.set_max_value(100.0)
progress_bar.set_bar_value(75.0)

# Change values with effects
progress_bar.decrease_bar_value(25.0)  # Triggers drain effects
progress_bar.increase_bar_value(10.0)

# Get current state
var current = progress_bar.get_current_value()
var percentage = progress_bar.get_percentage()
var is_full = progress_bar.is_full()


## Shader Parameters

### Bar Appearance
  * Bar Mode: Solid | RGB | Health Bar | Rainbow Wave | Fluid
  * Fill Mode: Discrete | Fade | Pour
  * Segment Count: Number of segments (1-50)
  * Colors: Background, filled, border, flash colors

### Visual Effects
  * Effect Mode: None | Wave | Bubbles | Glitch | Static | Pixel Static
  * Effect Strength: Intensity of the effect (0.0-3.0)
  * Animation Speed: Speed of animated effects

### Layout
  * Segment Gap: Space between segments
  * Border Size: Thickness of borders
  * Slant Amount: Slant the bar (-0.5 to 0.5)

## Script Configuration

### Flow Modes
  * Continuous: Smooth transitions for any value changes
  * Discrete: Step-by-step segment changes

### Fill Types  
  * Pour&Step: Bar fills like liquid pouring
  * Fade: Segments fade in/out gradually

### Effects
  * Flash: Segments flash white when losing value
  * Drain: Shows draining animation with customizable colors
  * Drain Solid: Solid color drain effect

## Signals

-----------------------------------------------------------------------
|  signal value_changed(old_value: float, new_value: float)           |
|  signal value_depleted()  # When bar reaches 0                      |
|  signal value_maxed()     # When bar reaches maximum                |
|  signal segment_lost(segment_index: int)                            |
|  signal segment_gained(segment_index: int)                          |
-----------------------------------------------------------------------

## Common Use Cases

### Health Bar
---------------------------------------------------------------------------------
|  # Set up health bar                                                          |
|  health_bar.material.set_shader_parameter("bar_mode", 2)  # Health Bar mode   |
|  health_bar.set_max_value(100.0)                                              |
|  health_bar.flow_mode = "Continuous"                                          |
|  health_bar.effect_type = "Flash"                                             |
---------------------------------------------------------------------------------

### XP/Level Bar
---------------------------------------------------------------------------------
|  # Set up XP bar with segments                                                |
|  xp_bar.material.set_shader_parameter("segment_count", 10)                    |
|  xp_bar.flow_mode = "Discrete"                                                |
|  xp_bar.fill_type = "Pour&Step"                                               |
---------------------------------------------------------------------------------

### Mana/Energy Bar
---------------------------------------------------------------------------------
|  # Set up mana bar with fluid effect                                          |
|  mana_bar.material.set_shader_parameter("bar_mode", 4)  # Fluid mode          |
|  mana_bar.material.set_shader_parameter("effect_mode", 2)  # Bubbles          |
---------------------------------------------------------------------------------

## Custom Frames

1. Enable custom frame in shader parameters
2. Assign your frame texture
3. Adjust scan steps (5-60) until bar fits properly
4. Fine-tune with trim, smoothness, and expansion settings

## Important Notes

- For discrete mode with segments, ensure your max values divide evenly by segment count for consistent behavior
- Flash/drain effects work best with Pour mode, limited support with Fade mode
- Single segment bars can use all fill modes effectively
- Use "set_bar_value(value, false)" to change values without triggering effects

## File Structure

- "progress_bar.gdshader" - Main shader with all visual effects
- "progress_bar.gd" - Controller script with game integration
- "player_example.gd" - Example usage showing health/mana/XP bars
- "demo_controller.gd" - Script used to demosntrate multiple bar modes and effects

## Performance Tips

- Higher segment counts require more processing
- Fluid mode is more performance intensive
- Multiple active effects can impact frame rate
- Use discrete mode for better performance with many segments
