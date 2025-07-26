# SCML Parser

**SCML Parser** is a tool to import Spriter `.scml` animations directly into Defold as `.collection` files.

![Defold](https://img.shields.io/badge/engine-Defold-blue?logo=defold&style=flat-square)
![Status](https://img.shields.io/badge/status-experimental-orange?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

---

## 🎥 Getting Started

<iframe width="560" height="315" src="https://www.youtube.com/embed/f2lc-fGAcvs?si=WxSLMP-BY2QeZAf3" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>



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

5. Done! You can now delete the `.scml` file if you want.  
   Simply add the generated `.collection` to your game scene.

---

## ⚙️ Script Properties

The generated collection has a script attached with properties.  
These include the **initial animation** to play and whether it should auto-play.  
Adjust these as needed, or uncheck **"Run"** to disable auto-start.

---

## 💬 Messages

You can control the animation using Defold’s message system:

- **Play an animation:**

  ```lua
  msg.post("your_collection_name", hash("run_animation"), {animation = "animation_name", loop = false})
  ```
  
- **Stop the current animation:**

  ```lua
  msg.post("your_collection_name", hash("cancel_animation"))
  ```

- **Get available animations and respond to the sender as array:**

  ```lua
  msg.post("your_collection_name", hash("list_animations"))
  ```

- **Get available character maps and respond to the sender as array:**

  ```lua
  msg.post("your_collection_name", hash("list_character_maps"))
  ```

- **Apply a sequence of character maps:**

  ```lua
  msg.post("your_collection_name", hash("apply_character_maps"), {"myCharmap1", "Charmap 2", --[[...]] })
  ```

- **Reset all character maps:**

  ```lua
  msg.post("your_collection_name", hash("reset_character_maps"))
  ```

- **Flip the animation horizontally:**

  ```lua
  msg.post("your_collection_name", hash("hflip_animation"), {flip = true})
  ```

> You can also instantiate multiple instances of the generated collection using Defold’s collectionfactory.
> Refer to the Defold documentation for more details.

---

## 🧪 Status

This is an initial but functional version of SCML Parser.
Bugs and limitations may exist — please report any issues with as much detail as possible.

---

## 📝 License

This project is licensed under the MIT License. See the LICENSE file for details.
