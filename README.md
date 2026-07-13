# SCML Parser

**SCML Parser** is a tool to import Spriter `.scml` animations directly into Defold as `.collection` files.

![Defold](https://img.shields.io/badge/engine-Defold-blue?logo=defold&style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

---

## 🎥 Getting Started

[<img src="https://img.youtube.com/vi/f2lc-fGAcvs/hqdefault.jpg" width="600" height="300"/>](https://www.youtube.com/embed/f2lc-fGAcvs?si=WxSLMP-BY2QeZAf3)

## 📦 Installation

You can install SCMLParser as a dependency in your project by doing the following:

1. In Defold, open your `game.project`.
2. Go to the **Projects** tab, under **Dependencies**, and click the **+** button.
3. Replace the `https://url.to/library` field with

   ```
   https://github.com/EVEVGames/SCMLParser/archive/refs/heads/main.zip
   ```
4. Save the project (important!).
5. From the menu, select **Project → Fetch Libraries**.


---

## 🚀 How to Use

1. Put your `.scml` file and all associated animation images in a **dedicated folder** inside your Defold project assets.  
   ⚠️ **Important:** Use a dedicated folder to avoid overwriting existing files.

2. Right-click the `.scml` file in the Assets panel.

3. Click **"Parse SCML"**.

4. A new `.collection`, a `.script`, and an `.atlas` will be generated in the same folder.  
   If files with the same names exist, they will be **overwritten**.  
   The console prints the path of the generated collection and its default animation.

5. Done! You can now delete the `.scml` file if you want.  
   Simply add the generated `.collection` to your game scene.

---

## ⚙️ Script Properties

The generated collection has a script attached with the following properties:

| Property | Description |
| --- | --- |
| **Run** | Auto-play the initial animation on startup. Uncheck to start paused. |
| **Animation** | The initial animation to play. |
| **Loop** | Whether the initial animation loops. Defaults to the animation's Spriter looping flag. |
| **Alpha Factor** | Multiplier applied to every sprite's alpha. |
| **Z Factor** | Multiplier applied to each sprite's z-index, setting the spacing between layers. |

---

## 💬 Control Messages

Control the animation using Defold's message system:

- **Play an animation:**

  ```lua
  msg.post("your_collection_name", "run_animation", {animation = "animation_name", loop = false})
  ```

- **Stop the current animation:**

  ```lua
  msg.post("your_collection_name", "cancel_animation")
  ```

- **Get available animations (replied to the sender as an array):**

  ```lua
  msg.post("your_collection_name", "list_animations")
  ```

- **Get available character maps (replied to the sender as an array):**

  ```lua
  msg.post("your_collection_name", "list_character_maps")
  ```

- **Apply a sequence of character maps:**

  ```lua
  msg.post("your_collection_name", "apply_character_maps", {"myCharmap1", "Charmap 2", --[[...]] })
  ```

- **Reset all character maps:**

  ```lua
  msg.post("your_collection_name", "reset_character_maps")
  ```

- **Flip the animation horizontally:**

  ```lua
  msg.post("your_collection_name", "hflip_animation", {flip = true})
  ```

> You can also instantiate multiple instances of the generated collection using Defold's collectionfactory.
> Refer to the Defold documentation for more details.

---

## 📡 Events

The animation broadcasts events during playback. They are always posted to the
animation's own game object, so a sibling `.script` receives them automatically. Other
game objects can receive them by subscribing (see below).

| Event | Payload |
| --- | --- |
| **animation_start** | `animation`, `loop`, `collection` |
| **animation_end** | `animation`, `loop`, `collection` |
| **animation_tag** | `animation`, `time`, `tags` (array), `collection` |
| **animation_object_tag** | `animation`, `name`, `time`, `tags` (array), `object`, `collection` |

`animation_tag` fires for animation-level Spriter taglines; `animation_object_tag`
fires for taglines placed on an individual object timeline and includes the `object`
url of the sprite active at that time. `collection` is the url of the animation game
object, and `object` the url of the tagged sprite — use them to read or change
transforms of the running animation. `animation_start` and `animation_end` fire on
every playback (and every loop cycle).

Handle events in `on_message`:

```lua
function on_message(self, message_id, message, sender)
    if message_id == hash("animation_tag") then
        for _, tag in ipairs(message.tags) do
            print(message.animation, "tag:", tag, "at", message.time)
        end
    elseif message_id == hash("animation_end") then
        -- message.animation, message.loop, message.collection
    end
end
```

### Subscribing from another game object

To receive events on a game object other than the animation's own, subscribe first:

- **Subscribe / unsubscribe the sender:**

  ```lua
  msg.post("your_collection_name", "subscribe")
  msg.post("your_collection_name", "unsubscribe")
  ```

- **List current subscribers (replied to the sender as an array):**

  ```lua
  msg.post("your_collection_name", "list_subscribers")
  ```

---

## 📝 License

This project is licensed under the MIT License. See the LICENSE file for details.
