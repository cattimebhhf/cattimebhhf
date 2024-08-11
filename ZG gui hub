# ZG gui hub

## screen gui
```lua
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ExampleGui"
screenGui.Parent = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")
```

## frame
```lua
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0.5, 0, 0.5, 0)
frame.Position = UDim2.new(0.25, 0, 0.25, 0)
frame.BackgroundTransparency = 1
frame.Parent = screenGui

--[[
BackgroundTransparency = 1-10
]]
```

## slide button
```lua
local UIS = game:GetService("UserInputService")
```

## pos you button
```lua
local function makeButton(name, text, position, parent)
    local button = Instance.new("TextButton")
    button.Name = name
    button.Size = UDim2.new(0.3, 0, 0.2, 0)
    button.Position = position
    button.Text = text
    button.BackgroundTransparency = 1 -- ทำให้ปุ่มโปร่งใส
    button.TextScaled = true -- ขยายข้อความให้เต็มปุ่ม
    button.TextColor3 = Color3.new(1, 1, 1) -- ตั้งค่าสีข้อความเป็นสีขาว
    button.Parent = parent

    local dragging, dragInput, dragStart, startPos

    local function update(input)
        local delta = input.Position - dragStart
        button.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end

    button.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = button.Position

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    button.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)

    UIS.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            update(input)
        end
    end)

    return button
end
```

## button
```lua
local button1 = makeButton("Button1", "name", UDim2.new(0.35, 0, 0.4, 0), frame)

button1.MouseButton1Click:Connect(function()
    your script
end) 

local button2 = makeButton("Button2", "name", UDim2.new(0.35, 0, 0.1, 0), frame)

button2.MouseButton2Click:Connect(function()
    your script
end) 
```
