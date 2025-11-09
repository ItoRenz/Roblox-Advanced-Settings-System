# Advanced Settings System for Roblox

A modular settings menu system for Roblox with Gameplay, Music, SFX, Audio, and Graphics tabs.

![Version](https://img.shields.io/badge/version-1.0.0-blue) ![Roblox](https://img.shields.io/badge/Roblox-Compatible-green) ![License](https://img.shields.io/badge/license-MIT-orange)

## ✨ Features

- **Modular Tab System** - Easy to add/remove tabs
- **Mobile & Desktop Support** - Responsive UI
- **DataStore Integration** - Auto-save settings
- **5 Built-in Tabs** - Gameplay, Music, SFX, Audio, Graphics
- **Global API** - Access via `_G.AdvancedSettings`

## 🏗️ Structure
```
StarterPlayerScripts/AdvancedSettings/
├── Main (LocalScript)
├── LoadTabs (LocalScript)
└── Tabs/
    ├── GameplayTab (ModuleScript)
    ├── MusicTab (ModuleScript)
    ├── SFXTab (ModuleScript)
    ├── AudioTab (ModuleScript)
    └── GraphicsTab (ModuleScript)

ServerScriptService/
└── MusicPlayerServer (Script)
```

## 📦 Installation

1. **Create folder structure** in `StarterPlayerScripts`
2. **Copy scripts** to respective locations
3. **Enable DataStore**: Game Settings > Security > Enable API Services
4. **Publish game** for DataStore to work

## 📑 Tab Overview

### 🎮 Gameplay
- Hide Title/Players/UI
- Spectator Mode (◀ ▶)
- Reset to Base

### 🎵 Music
- Custom playlist with favorites
- Play/Pause/Skip controls
- Shuffle & Loop modes
- Volume control (0-10)
- DataStore persistence

### 🔊 SFX
- **Jump Sounds**: Unyah, Mario, 8-Bit
- **Walk Sounds**: Cit Cit, Squidward, SpongeBob, Mr. Krabs
- Master toggle

### 🎚️ Audio
- Master/Music/SFX/UI volume sliders
- Real-time sound tracking
- Zero-jitter controls

### 📊 Graphics
- 5 presets (Lowest to Highest)
- Real-time FPS/Ping/Memory monitor
- Performance rating

## 🔧 Add Custom Tab

**Create Tab Module:**
```lua
local YourTab = {}

function YourTab.createContent(contentScroll, colors, isMobile, utils)
    -- Build UI here
end

function YourTab.setup()
    print("✅ Tab setup")
end

function YourTab.cleanup()
    print("🧹 Cleanup")
end

return YourTab
```

**Register in LoadTabs:**
```lua
local YourTab = require(script.Parent.Tabs.YourTab)
_G.AdvancedSettings.registerTab(
    "YOUR_TAB", "Your Tab", 6,
    YourTab.createContent, YourTab.setup, YourTab.cleanup
)
```

## 📚 Quick API
```lua
-- Toggle menu
_G.AdvancedSettings.toggleMenu()

-- Audio control
_G.AdvancedSettings.AudioManager:setMasterVolume(8)
_G.AdvancedSettings.AudioManager:setMusicVolume(5)

-- Music control
_G.AdvancedSettings.MusicPlayer:play()
_G.AdvancedSettings.MusicPlayer:next()

-- Utilities
_G.AdvancedSettings.utils.corner(frame, 10)
_G.AdvancedSettings.utils.tween(frame, TweenInfo.new(0.3), {Size = UDim2.new(1,0,1,0)})

-- Check device
if _G.AdvancedSettings.isMobile then print("Mobile") end
```

## ⚙️ Configuration

**Colors (Main.lua):**
```lua
local Colors = {
    bg = Color3.fromRGB(44,47,51),
    accent = Color3.fromRGB(255,204,92),
    text = Color3.fromRGB(255,255,255),
    good = Color3.fromRGB(120,220,120)
}
```

**DataStore (MusicPlayerServer.lua):**
```lua
local CONFIG = {
    DATASTORE_NAME = "MusicPlayerData_v2",
    AUTOSAVE_INTERVAL = 180,
    MAX_CUSTOM_SONGS = 100,
    DEBUG_MODE = false
}
```

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| Menu won't open | Check console errors, verify script locations |
| Tabs not showing | Check registration in LoadTabs, verify module returns |
| Music not saving | Enable DataStore in Game Settings, publish game |
| Sounds not playing | Check Asset IDs, verify master toggle is ON |
| Slider jittering | Use latest code (v1.0.0 fixed this) |

**Debug Mode:**
```lua
-- In MusicPlayerServer.lua
DEBUG_MODE = true  -- See detailed logs
```

**Console Commands:**
```lua
print(#_G.AdvancedSettings.tabs)  -- Count tabs
_G.AdvancedSettings.toggleMenu()  -- Force toggle
```

## 📊 Performance

| Scenario | FPS | Memory |
|----------|-----|--------|
| Menu Closed | 60 | ~50 MB |
| Menu Open | 58 | ~65 MB |
| All Active | 55 | ~80 MB |

## 🎨 Custom Components

**Toggle Button:**
```lua
local function createToggle(parent, colors, isMobile, utils)
    local bg = Instance.new("Frame")
    bg.Size = UDim2.new(0, isMobile and 32 or 38, 0, isMobile and 16 or 20)
    bg.BackgroundColor3 = colors.toggleOff
    utils.corner(bg, 10)
    
    local knob = Instance.new("Frame")
    knob.Size = UDim2.new(0, isMobile and 12 or 16, 0, isMobile and 12 or 16)
    knob.BackgroundColor3 = colors.text
    knob.Parent = bg
    utils.corner(knob, 8)
    
    return bg, knob
end
```

## 📄 License

MIT License - Copyright (c) 2024 ItoRenz00

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software.

## 👤 Author

**ItoRenz00**
- Roblox Developer & UI/UX Specialist
- GitHub: [@ItoRenz](https://github.com/ItoRenz)

## 🙏 Credits

- **ItoRenz00** - System creator and developer
- **Roblox Community** - Testing and feedback
- **Contributors** - Bug fixes and improvements

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/ItoRenz00/AdvancedSettings/issues)
- **Docs**: Check README and code comments
- **Contact**: Via GitHub or Roblox messages

Include in reports:
- Roblox Studio version
- Error messages
- Steps to reproduce
- Screenshots

## 🔗 Resources

- [Roblox Developer Hub](https://create.roblox.com/docs)
- [DevForum](https://devforum.roblox.com/)
- [TweenService Docs](https://create.roblox.com/docs/reference/engine/classes/TweenService)
- [DataStore Guide](https://create.roblox.com/docs/cloud-services/data-stores)

## 📝 Best Practices

✅ **DO:**
- Use `pcall()` for error handling
- Clean up connections in `cleanup()`
- Use provided utilities
- Test on mobile and PC
- Comment complex code

❌ **DON'T:**
- Skip error handling
- Forget cleanup
- Hardcode values
- Ignore mobile support

## 🚀 Quick Start
```lua
-- Access system
local settings = _G.AdvancedSettings

-- Open menu
settings.toggleMenu()

-- Set audio
settings.AudioManager:setMasterVolume(8)

-- Play music
settings.MusicPlayer:play()

-- Check device
if settings.isMobile then
    print("Mobile UI")
end
```

---

**Made with ❤️ by ItoRenz00**

*If this helped your game, give it a ⭐ on GitHub!*
