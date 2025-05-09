<img src="Assets/logodark.png#gh-dark-mode-only" alt="fluent">
<img src="Assets/logolight.png#gh-light-mode-only" alt="fluent">

## ⚡ Features

- Modern, **fluent**-style design  
- Highly **customizable**: themes, sizes, acrylic blur  
- Complete set of **UI elements**: windows, tabs, paragraphs, buttons, toggles, sliders, dropdowns (single/multi), color pickers (with transparency), keybinds, inputs, dialogs, notifications  
- Built-in **SaveManager** and **InterfaceManager** addons  

## 🔌 Installation

```lua
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
Optionally load the addons:

lua
Copy
Edit
local SaveManager      = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()
📜 Usage
lua
Copy
Edit
-- Initialize Fluent & Addons
local Fluent           = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager      = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

-- Create Main Window
local Window = Fluent:CreateWindow({
    Title        = "Fluent " .. Fluent.Version,
    SubTitle     = "by dawid",
    TabWidth     = 160,
    Size         = UDim2.fromOffset(580, 460),
    Acrylic      = true,
    Theme        = "Dark",
    MinimizeKey  = Enum.KeyCode.LeftControl,
})

-- Add Tabs
local Tabs = {
    Main     = Window:AddTab({ Title = "Main",     Icon = ""         }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" }),
}

-- Quick Notification
Fluent:Notify({
    Title      = "Welcome!",
    Content    = "Fluent UI is ready to use.",
    SubContent = "Customize it however you like.",
    Duration   = 5,
})
# Paragraph
lua
Copy
Edit
Tabs.Main:AddParagraph({
    Title   = "Introduction",
    Content = "This is a paragraph.\nYou can put multiple lines!",
})
# Button
lua
Copy
Edit
Tabs.Main:AddButton({
    Title       = "Show Dialog",
    Description = "Opens a simple dialog window",
    Callback    = function()
        Window:Dialog({
            Title   = "Dialog Title",
            Content = "This is the dialog content.",
            Buttons = {
                { Title = "Confirm", Callback = function() print("Confirmed!") end },
                { Title = "Cancel",  Callback = function() print("Cancelled!") end },
            },
        })
    end,
})
# Toggle
lua
Copy
Edit
local MyToggle = Tabs.Main:AddToggle("MyToggle", {
    Title   = "Enable Feature",
    Default = false,
})
MyToggle:OnChanged(function()
    print("Toggle is now:", MyToggle.Value)
end)
# Slider
lua
Copy
Edit
local MySlider = Tabs.Main:AddSlider("Slider", {
    Title       = "Adjust Value",
    Description = "Range: 0–5",
    Default     = 2,
    Min         = 0,
    Max         = 5,
    Rounding    = 1,
    Callback    = function(val) print("Slider:", val) end,
})
MySlider:SetValue(3)
# Dropdown (single-select)
lua
Copy
Edit
local DD = Tabs.Main:AddDropdown("Dropdown", {
    Title   = "Choose One",
    Values  = {"One","Two","Three","Four"},
    Multi   = false,
    Default = 1,
})
DD:OnChanged(function(val) print("Dropdown:", val) end)
# Dropdown (multi-select)
lua
Copy
Edit
local MDD = Tabs.Main:AddDropdown("MultiDropdown", {
    Title       = "Choose Multiple",
    Description = "Select as many as you like",
    Values      = {"A","B","C","D","E"},
    Multi       = true,
    Default     = {"A","C"},
})
MDD:OnChanged(function(vals)
    local t = {}
    for v,_ in pairs(vals) do table.insert(t, v) end
    print("MultiDropdown:", table.concat(t, ", "))
end)
# Color Picker
lua
Copy
Edit
local CP = Tabs.Main:AddColorpicker("Colorpicker", {
    Title   = "Pick a Color",
    Default = Color3.fromRGB(96,205,255),
})
CP:OnChanged(function() print("Color:", CP.Value) end)
CP:SetValueRGB(Color3.fromRGB(0,255,140))
# Color Picker with Transparency
lua
Copy
Edit
local TCP = Tabs.Main:AddColorpicker("TransColorpicker", {
    Title        = "Color + Transparency",
    Description  = "Slide to adjust alpha",
    Transparency = 0,
    Default      = Color3.fromRGB(96,205,255),
})
TCP:OnChanged(function()
    print("Color:", TCP.Value, "Alpha:", TCP.Transparency)
end)
# Keybind
lua
Copy
Edit
local KB = Tabs.Main:AddKeybind("Keybind", {
    Title           = "Press Key",
    Mode            = "Toggle",           -- "Hold", "Always", "Toggle"
    Default         = "LeftControl",
    Callback        = function(state) print("Keybind:", state) end,
    ChangedCallback = function(newKey) print("New Key:", newKey) end,
})
KB:OnClick(function() print("Key clicked, state:", KB:GetState()) end)
# Input Field
lua
Copy
Edit
local IN = Tabs.Main:AddInput("Input", {
    Title       = "Your Text",
    Default     = "Default",
    Placeholder = "Type here...",
    Numeric     = false,
})
IN:OnChanged(function() print("Input:", IN.Value) end)
# SaveManager & InterfaceManager
lua
Copy
Edit
-- Setup SaveManager & InterfaceManager
SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)
SaveManager:IgnoreThemeSettings()          -- don’t save theme changes
SaveManager:SetIgnoreIndexes({})           -- ignore specific element indexes

InterfaceManager:SetFolder("MyScriptHub") -- top-level folder
SaveManager:SetFolder("MyScriptHub/Game1")
InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)

Window:SelectTab(1)
# Final Notification & Autoload
lua
Copy
Edit
Fluent:Notify({ Title = "All Set!", Content = "Fluent is fully configured.", Duration = 8 })
SaveManager:LoadAutoloadConfig()   -- will auto-load if marked so
Credits
richie0866/remote-spy – UI assets & helper utilities

violin-suzutsuki/LinoriaLib – core element implementations & save manager

7kayoh/Acrylic – acrylic blur module port

Latte Softworks & Kotera – bundler maintenance (via Discord)

Copy
Edit
