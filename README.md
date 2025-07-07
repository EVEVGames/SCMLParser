# DeSpriter

**DeSpriter** is a tool to import Spriter `.scml` animations directly into Defold as `.collection` files.

![Defold](https://img.shields.io/badge/engine-Defold-blue?logo=defold&style=flat-square)
![Status](https://img.shields.io/badge/status-experimental-orange?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

---

## 📦 Installation

1. Place the `DeSpriter.editor_script` file into any folder inside your Defold project's `assets`.
2. Restart Defold, or press `Ctrl+Shift+R` (`Cmd+Shift+R` on macOS) to reload the editor script.

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
Adjust these as needed, or uncheck **"Play"** to disable auto-start.

---

## 💬 Messages

You can control the animation using Defold’s message system:

- **Play an animation:**

  ```lua
  msg.post("your_collection_name", "play_animation", { animation = "animation_name", loop = false })
  ```
  
- **Stop the current animation:**

  ```lua
  msg.post("your_collection_name", "stop_animation")
  ```

> You can also instantiate multiple instances of the generated collection using Defold’s collectionfactory.
> Refer to the Defold documentation for more details.

---

## 🧪 Status

This is an initial but functional version of DeSpriter.
Bugs and limitations may exist — please report any issues with as much detail as possible.

---

## 📝 License

This project is licensed under the MIT License. See the LICENSE file for details.
