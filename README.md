## 🚀 Dash System — Roblox Gameplay Mechanic  
A lightweight, modular dash mechanic built for Roblox Studio.  
Designed for responsiveness, clean architecture and easy integration into any character controller.

---

## 📌 Overview  
This project implements a compact but production‑ready **Dash System** featuring:

- client‑side VFX and SFX  
- server‑validated movement  
- smooth velocity decay  
- modular functions for sound, force and effects  
- clean, readable Lua code suitable for gameplay engineering portfolios  

Originally created as part of my exploration into building responsive movement mechanics and improving game feel inside Roblox Studio.

---

## ✨ Features  
- **Instant dash impulse** with smooth falloff  
- **Custom SFX** using a user‑provided sound asset  
- **Multiple particle layers** (flash, trail, dust, smoke, sparks)  
- **Client–server separation** for security and performance  
- **Minimalistic API** — two main functions:  
  - `playDashSound()`  
  - `applyDashForce()`  
- Zero dependencies, plug‑and‑play

---

## 🧠 Tech Breakdown  
This system demonstrates several gameplay engineering concepts:

### Client‑side:
- Input handling  
- Local VFX spawning  
- Local SFX playback  
- Smooth velocity decay  
- Attachments and particle emitters  
- Trail generation  

### Server‑side:
- Validated dash impulse  
- BodyVelocity injection  
- Cleanup via `Debris`  

### Architecture:
- Functions are isolated and reusable  
- No hard‑coded character references  
- Clean separation of responsibilities  
- Lightweight and performant  

---

## 🧩 Code Structure  

```
/src
 ├── DashClient.lua     -- client-side logic, VFX, SFX, input
 ├── DashServer.lua     -- server-side movement validation
 └── README.md          -- documentation
```

---

## 🧪 Core Functions (from LinkedIn post)

```lua
local function playDashSound()
    local s = Instance.new("Sound")
    s.SoundId = "rbxassetid://140185787227440"
    s.Volume = 1.5
    s.PlaybackSpeed = 1.15
    s.Parent = root
    s:Play()
    game.Debris:AddItem(s, 2)
end

local function applyDashForce()
    local bv = Instance.new("BodyVelocity")
    bv.MaxForce = Vector3.new(2e6, 0, 2e6)
    bv.Velocity = root.CFrame.LookVector * 110

    bv.Parent = root

    task.spawn(function()
        for i = 1, 5 do
            task.wait(0.04)
            bv.Velocity *= 0.75
        end
    end)

    game.Debris:AddItem(bv, 0.25)
end
```

---

## ⚙️ How It Works  
1. Player presses the dash key  
2. Client triggers:  
   - sound  
   - particles  
   - local velocity smoothing  
3. Client sends a request to the server  
4. Server applies a validated impulse  
5. Debris cleans up temporary objects  

This ensures responsiveness **and** security.

---

## 📥 Installation  
1. Copy `DashClient.lua` into:  
   ```
   StarterPlayerScripts
   ```
2. Copy `DashServer.lua` into:  
   ```
   ServerScriptService
   ```
3. Add a `RemoteEvent` named `DashEvent` into:  
   ```
   ReplicatedStorage
   ```
4. Replace the sound ID with your own if needed.

---

## ▶️ Usage  
Press **Q** to dash.  
All effects, sound and movement will trigger automatically.

---

## 🔮 Future Improvements  
- Directional dash (WASD)  
- Camera shake  
- Afterimage ghost trail  
- Hit detection during dash  
- Cooldown UI  
- Animation blending  
