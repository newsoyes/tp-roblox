# 🌐 NEWSOYES — Roblox Teleportation GUI

<div align="center">

![Roblox](https://img.shields.io/badge/Roblox-Luau-00A2FF?style=for-the-badge&logo=roblox&logoColor=white)
![Script Type](https://img.shields.io/badge/Script-Client%20Side%20GUI-blueviolet?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge)

**A dynamic, draggable, and animated client-side Teleportation Tool for Roblox.**  
*สคริปต์ UI วาร์ปพิกัดแบบไดนามิก รองรับการลาก พับเก็บ และเปลี่ยนสีพื้นหลังอัตโนมัติ สำหรับ Roblox*

[English](#-english-documentation) • [ภาษาไทย](#-เอกสารภาษาไทย)

---

</div>

## 📑 Table of Contents / สารบัญ

- [English Documentation](#-english-documentation)
  - [Overview](#-overview)
  - [Key Features](#-key-features)
  - [UI Layout & Controls](#-ui-layout--controls)
  - [How to Use](#-how-to-use)
  - [Technical Details](#-technical-details)
  - [Configuration & Tweaks](#-configuration--tweaks)
- [เอกสารภาษาไทย](#-เอกสารภาษาไทย)
  - [ภาพรวมโครงการ](#-ภาพรวมโครงการ)
  - [จุดเด่นและฟังก์ชันหลัก](#-จุดเด่นและฟังก์ชันหลัก)
  - [ส่วนประกอบของหน้าต่างเมนู](#-ส่วนประกอบของหน้าต่างเมนู)
  - [วิธีนำไปใช้งาน](#-วิธีนำไปใช้งาน)
  - [เจาะลึกการทำงานของโค้ด](#-เจาะลึกการทำงานของโค้ด)
  - [คำแนะนำเพิ่มเติมและการปรับแต่ง](#-คำแนะนำเพิ่มเติมและการปรับแต่ง)
- [⚠️ Disclaimer / ข้อควรระวัง](#️-disclaimer--ข้อควรระวัง)
- [📄 License](#-license)

---

# 🇬🇧 English Documentation

## 🌟 Overview

**NEWSOYES Teleport GUI** is a lightweight, responsive client-side utility written in Luau for Roblox. It enables players to instantly teleport their characters via manual coordinate input $(X, Y, Z)$ or predefined preset buttons, all wrapped inside a sleek, animated user interface.

---

## ✨ Key Features

| Feature | Description |
| :--- | :--- |
| 🌈 **RGB Background Animation** | Smoothly interpolates background colors infinitely using Roblox's `TweenService`. |
| 🖐️ **Smooth Window Dragging** | Fully draggable window that can be freely repositioned anywhere on the screen. |
| 📦 **Minimize & Restore** | Collapse the interface into a compact indicator icon to declutter the viewport. |
| 📍 **Custom Coordinates Teleport** | Input arbitrary $X, Y, Z$ positions to warp instantly. |
| ⚡ **Preset Shortcuts** | One-click teleportation to fixed destination coordinates (e.g., Pirate Island: `-2825, 214, 1517`). |
| ❌ **Quick Exit** | Dedicated close button to clean up and destroy the GUI safely from memory. |

---

## 🖥️ UI Layout & Controls

```
+----------------------------------------------------+
|  [NEWSOYES]                             [-]   [X]  |  <- Header (Title, Minimize, Close)
+----------------------------------------------------+
|  [ X: Coordinate Input Box                      ]  |
|  [ Y: Coordinate Input Box                      ]  |
|  [ Z: Coordinate Input Box                      ]  |
|  [ 🟢 Warp (Teleport to Input)                 ]  |
|  [ 🔵 Pirate (Preset Teleport)                 ]  |
+----------------------------------------------------+
```

* **Header Controls**:
  * `_` *(Blue Button)*: Minimizes the UI into a compact red floating indicator box.
  * `ปิด` *(Red Button)*: Destroys the `ScreenGui` instance and cleans up UI assets.
* **Teleportation**:
  * `วาร์ป` *(Green Button)*: Parses $X, Y, Z$ text inputs into floating-point numbers and updates the player's `HumanoidRootPart.CFrame`.
  * `โจรสลัด` *(Blue Button)*: Instantly sets character coordinates to `CFrame.new(-2825, 214, 1517)`.

---

## 🚀 How to Use

### Method 1: Roblox Studio (Testing & Development)
1. Open your project in **Roblox Studio**.
2. In the **Explorer** window, navigate to `StarterPlayer` > `StarterPlayerScripts` (or `StarterGui`).
3. Create a new `LocalScript`.
4. Paste the contents of `script.lua` into your new script.
5. Press **Play (F5)** to test the GUI in-game.

### Method 2: In-Game Script Execution (Client-side)
1. Launch the target Roblox experience.
2. Inject your preferred environment or executor.
3. Paste the contents of `script.lua` into the script executor.
4. Execute the script; the menu will immediately appear in the center of your screen.

---

## ⚙️ Technical Details

- **Language**: Luau / Lua 5.1
- **Key Services**:
  - `TweenService`: Powers seamless RGB transitions with linear easing over 2-second cycles.
  - `game.Players.LocalPlayer`: Dynamically targets the executing client.
  - `UserInputService` / Direct Input Listeners: Handles window drag offsets and click interactions.
- **Position Handling**:
  - Manipulates the `CFrame` of `Character.HumanoidRootPart` to achieve immediate position translation without physics lag.

---

## 💡 Configuration & Tweaks

### Adjusting UI Height
In the original script, the `pirateButton` is positioned at $Y = 210$, while the frame height is set to $200$. To prevent overflow clipping, you can adjust the frame height:
```lua
-- Change:
frame.Size = UDim2.new(0, 300, 0, 200)

-- Recommended:
frame.Size = UDim2.new(0, 300, 0, 270)
```

### Adding New Presets
To add another quick-warp location, replicate the button template:
```lua
local newButton = Instance.new("TextButton")
newButton.Text = "Destination Name"
newButton.Size = UDim2.new(0, 260, 0, 40)
newButton.Position = UDim2.new(0, 20, 0, 260) -- Adjust Y position accordingly
newButton.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
newButton.Parent = frame

newButton.MouseButton1Click:Connect(function()
    local char = game.Players.LocalPlayer.Character
    if char and char:FindFirstChild("HumanoidRootPart") then
        char.HumanoidRootPart.CFrame = CFrame.new(0, 100, 0) -- Set custom X, Y, Z
    end
end)
```

---

# 🇹🇭 เอกสารภาษาไทย

## 🌟 ภาพรวมโครงการ

**NEWSOYES Teleport GUI** เป็นสคริปต์ส่วนติดต่อผู้ใช้ (UI) ฝั่ง Client เขียนด้วยภาษา Luau สำหรับแพลตฟอร์ม Roblox ช่วยให้ผู้เล่นสามารถวาร์ปตัวละครไปยังพิกัดที่กำหนดเอง $(X, Y, Z)$ หรือวาร์ปไปยังจุดพิกัดด่วนได้ในคลิกเดียว มาพร้อมกับดีไซน์ไฟ RGB แบบแอนิเมชัน และระบบการลาก/พับเก็บหน้าต่างที่ใช้งานง่าย

---

## ✨ จุดเด่นและฟังก์ชันหลัก

| ฟังก์ชัน | รายละเอียดการทำงาน |
| :--- | :--- |
| 🌈 **พื้นหลัง RGB ไล่เฉดสีอัตโนมัติ** | ใช้ `TweenService` สุ่มค่าสี RGB ทุกๆ 2 วินาที สลับสีไปมาอย่างนุ่มนวลตลอดเวลา |
| 🖐️ **ระบบลากย้ายหน้าต่าง (Draggable)** | สามารถคลิกค้างแล้วลากหน้าจอเมนูไปวางจุดใดก็ได้บนหน้าจอ |
| 📦 **พับและขยายหน้าต่าง (Minimize/Restore)** | กดปุ่มย่อหน้าต่างเป็นไอคอนสี่เหลี่ยมสีแดงขนาดกะทัดรัด และคลิกเพื่อขยายกลับมาได้ |
| 📍 **วาร์ปตามพิกัดอิสระ** | มีช่องกรอกค่าแกน $X, Y, Z$ และปุ่มสั่งวาร์ปไปยังตำแหน่งนั้นทันที |
| ⚡ **ปุ่มลัดวาร์ปด่วน (Preset)** | ปุ่มวาร์ปไปยังจุดเฉพาะ เช่น "โจรสลัด" (พิกัด: `-2825, 214, 1517`) ในคลิกเดียว |
| ❌ **ปุ่มปิดหน้าต่าง** | ปุ่ม "ปิด" สีแดง ลบ UI ออกจาก `PlayerGui` อย่างสมบูรณ์ |

---

## 🖥️ ส่วนประกอบของหน้าต่างเมนู

```
+----------------------------------------------------+
|  [NEWSOYES]                             [-]   [ปิด] |  <- แถบส่วนหัว
+----------------------------------------------------+
|  [ ช่องกรอกค่าแกน X                              ]  |
|  [ ช่องกรอกค่าแกน Y                              ]  |
|  [ ช่องกรอกค่าแกน Z                              ]  |
|  [ 🟢 วาร์ป (ไปยังพิกัด X, Y, Z ที่กรอก)          ]  |
|  [ 🔵 โจรสลัด (พิกัดลัด -2825, 214, 1517)         ]  |
+----------------------------------------------------+
```

### การควบคุมและการสั่งการ
1. **ปุ่ม `_` (พับหน้าต่าง)**: ซ่อนหน้าต่างหลัก และแสดงกล่องไอคอนสีแดงขนาด $40 \times 40$ พิกเซลแทน
2. **กล่องสีแดง (ขยายหน้าต่าง)**: คลิกที่กล่องนี้เพื่อเปิดหน้าต่างหลักกลับขึ้นมา
3. **ปุ่ม `ปิด` (สีแดง)**: สั่ง `screenGui:Destroy()` เพื่อปิดและนำสคริปต์ UI ออกจากหน้าจอ
4. **ปุ่ม `วาร์ป` (สีเขียว)**: นำตัวเลขจากช่อง $X, Y, Z$ ไปเปลี่ยนค่า `CFrame` ของ `HumanoidRootPart` ของตัวละคร
5. **ปุ่ม `โจรสลัด` (สีฟ้า)**: วาร์ปไปยังจุดพิกัด `CFrame.new(-2825, 214, 1517)` ทันที

---

## 🚀 วิธีนำไปใช้งาน

### วิธีที่ 1: ใช้งานใน Roblox Studio
1. เปิดโปรเจกต์ของคุณในโปรแกรม **Roblox Studio**
2. ไปที่หน้าต่าง **Explorer** แล้วหาโฟลเดอร์ `StarterPlayer` > `StarterPlayerScripts` (หรือ `StarterGui`)
3. คลิกขวาแล้วเลือก **Insert Object** > **LocalScript**
4. นำโค้ดในไฟล์ `script.lua` ไปวางทับในสคริปต์ดังกล่าว
5. กดปุ่ม **Play (F5)** เพื่อทดสอบการทำงาน

### วิธีที่ 2: รันผ่าน Script Executor (ฝั่ง Client)
1. เข้าเล่นเกม Roblox ที่ต้องการทดสอบ
2. เปิดโปรแกรม Executor ที่รองรับ
3. นำโค้ดทั้งหมดใน `script.lua` ไปวางในกล่องข้อความ
4. กด **Execute / Inject** เมนูจะปรากฏขึ้นกลางหน้าจอทันที

---

## ⚙️ เจาะลึกการทำงานของโค้ด

- **การเรนเดอร์ UI**: สร้าง `ScreenGui` และใส่ไว้ใน `PlayerGui` ของ `LocalPlayer`
- **ระบบไล่สีอัตโนมัติ (Color Tweening)**:
  ```lua
  local tween = TweenService:Create(frame, TweenInfo.new(2), {BackgroundColor3 = randomColor})
  ```
  ใช้ `spawn()` หรือการวนซ้ำ `while true` เพื่อสุ่มสี RGB และเล่น Tween อย่างต่อเนื่อง
- **กลไกการวาร์ปตัวละคร**:
  อ้างอิงผ่าน `character.HumanoidRootPart.CFrame` ซึ่งเป็นการย้ายตำแหน่งเชิงพิกัดโดยตรง (Instant Coordinate Translation) โดยไม่ทำให้ตัวละครติดบั๊กฟิสิกส์

---

## 💡 คำแนะนำเพิ่มเติมและการปรับแต่ง

### การปรับขนาดความสูงของหน้าต่าง (Frame Size)
ในโค้ดต้นฉบับ ขนาดความสูงของ Frame ถูกตั้งไว้ที่ `200` แต่ปุ่ม "โจรสลัด" วางอยู่ที่แกน $Y = 210$ ทำให้ปุ่มอาจจะล้นขอบออกมา แนะนำให้ปรับขนาดของ Frame ดังนี้:
```lua
-- โค้ดเดิม:
frame.Size = UDim2.new(0, 300, 0, 200)

-- แนะนำให้แก้ไขเป็น:
frame.Size = UDim2.new(0, 300, 0, 270)
```

### การเพิ่มจุดวาร์ปใหม่ๆ
หากต้องการเพิ่มปุ่มวาร์ปไปยังตำแหน่งอื่นๆ ในเกม สามารถคัดลอกตัวอย่างนี้ไปต่อท้ายได้:
```lua
local safeZoneButton = Instance.new("TextButton")
safeZoneButton.Text = "จุดปลอดภัย (Safe Zone)"
safeZoneButton.Size = UDim2.new(0, 260, 0, 40)
safeZoneButton.Position = UDim2.new(0, 20, 0, 260)
safeZoneButton.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
safeZoneButton.Parent = frame

safeZoneButton.MouseButton1Click:Connect(function()
    local character = game.Players.LocalPlayer.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        character.HumanoidRootPart.CFrame = CFrame.new(100, 50, 100) -- เปลี่ยนพิกัดตามต้องการ
    end
end)
```

---

## ⚠️ Disclaimer / ข้อควรระวัง

- **Terms of Service**: การใช้สคริปต์บุคคลที่สามผ่าน Executor ในเกมออนไลน์สาธารณะอาจละเมิดข้อกำหนดการให้บริการ (Terms of Service) ของ Roblox ผู้ใช้ควรรับผิดชอบต่อความเสี่ยงในการถูกระงับบัญชีด้วยตนเอง
- **Intended Purpose**: โค้ดนี้มีวัตถุประสงค์เพื่อการศึกษาและการพัฒนาเกมภายในสภาพแวดล้อมส่วนตัว (Roblox Studio) เท่านั้น

---

## 📄 License

This project is released under the **MIT License**. Feel free to modify, distribute, and integrate it into your own creations.
