# Free ZG gui hub

## description
```lua
นี้คือ gui อันสองของ ZG hub นะครับ ไว้รันสคริป
สร้างมาเพื่อความบันเทิง
```


## screen gui (need)
```lua
local screenGui = Instance.new("ScreenGui")
```
## screen name (need) 
```lua
screenGui.Name = "GUI v1.0"
```
## player gui (need)
```lua
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
```
## frame gui
```lua
-- ไว้โหลด เฟรมหรือพื้นหลัง
local frame = Instance.new("Frame")
-- ขนาดของพื้นหลัง
frame.Size = UDim2.new(0, 300, 0, 400)
-- ตำแหน่งของพื้นหลัง
frame.Position = UDim2.new(0.5, -150, 0.5, -200)
-- สีของพื้นหลัง
frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
-- ขนาด pixel 0นะครับ
frame.BorderSizePixel = 0
-- เชื่อมกับ screen gui 
frame.Parent = screenGui
-- การมอนเห็นพื้นหลัง![1000007550](https://github.com/user-attachments/assets/32653956-c592-40a9-8e2f-555e0b5fc57a)

frame.Visible = true -- true =เปิด/false =ปิด
```
## สีสลับ ของ background
```lua
local gradient = Instance.new("UIGradient")
gradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 0, 0)), -- สีขวา
    ColorSequenceKeypoint.new(1, Color3.fromRGB(0, 0, 0))    -- สีซ้าย
}
gradient.Parent = frame
```
## ขอบวงกลม (จะมีหรือไม่ก็ได้)
```lua
local frameCorner = Instance.new("UICorner")
frameCorner.CornerRadius = UDim.new(0, 20)
frameCorner.Parent = frame
```
## text box (ไว้ใส่สคริป)
```lua
local textBox = Instance.new("TextBox")
textBox.Size = UDim2.new(1, -10, 0, 300)
textBox.Position = UDim2.new(0, 5, 0, 5)
textBox.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
textBox.BorderSizePixel = 0
textBox.Text = "Insert your script here..."
textBox.TextColor3 = Color3.fromRGB(255, 255, 255)
textBox.TextScaled = true
textBox.TextWrapped = true
textBox.MultiLine = true
textBox.ClearTextOnFocus = false
textBox.Parent = scrollBox
```
## ปุ่มรันสคริป
```lua
local executeButton = Instance.new("TextButton")
executeButton.Size = UDim2.new(0, 120, 0, 40)
executeButton.Position = UDim2.new(0.3, -60, 0.75, 0)
executeButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
executeButton.Text = "Execute"
executeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
executeButton.TextScaled = true
executeButton.Font = Enum.Font.SourceSansBold
executeButton.Parent = frame
```

## ขอบวงกลม ของปุ่ม
```lua
local buttonCorner = Instance.new("UICorner")
buttonCorner.CornerRadius = UDim.new(0, 15)
buttonCorner.Parent = executeButton
```

## ปุ่ม clear ไว้ลบสคริปใน text box
```lua
local clearButtonCorner = Instance.new("UICorner")
clearButtonCorner.CornerRadius = UDim.new(0, 15)
clearButtonCorner.Parent = clearButton
```

## ขอบวงกลม ของปุ่ม
```lua
local clearButtonCorner = Instance.new("UICorner")
clearButtonCorner.CornerRadius = UDim.new(0, 15)
clearButtonCorner.Parent = clearButton
```

## ฟั่งชั่นของปุ่ม clear
```lua
clearButton.MouseButton1Click:Connect(function()
    textBox.Text = ""
end)
```

## ปุ่มย่อขนาด gui
```lua
local minimizeButton = Instance.new("TextButton")
minimizeButton.Size = UDim2.new(0, 30, 0, 30)
minimizeButton.Position = UDim2.new(1, -35, 0, 5)
minimizeButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)
minimizeButton.Text = "-"
minimizeButton.TextColor3 = Color3.fromRGB(0, 0, 0)
minimizeButton.TextScaled = true
minimizeButton.Font = Enum.Font.SourceSansBold
minimizeButton.Parent = frame
```

## ฟั่งชั่นย่อขนาด
```lua
local isMinimized = false
minimizeButton.MouseButton1Click:Connect(function()
    if isMinimized then
        frame.Size = UDim2.new(0, 300, 0, 400)
        scrollBox.Visible = true
        executeButton.Visible = true
        clearButton.Visible = true
        isMinimized = false
    else
        frame.Size = UDim2.new(0, 300, 0, 50)
        scrollBox.Visible = false
        executeButton.Visible = false
        clearButton.Visible = false
        isMinimized = true
    end
end)
```

## label แสดงสถานะ
```lua
local statusLabel = Instance.new("TextLabel")
statusLabel.Size = UDim2.new(1, -20, 0, 20)
statusLabel.Position = UDim2.new(0, 10, 1, -30)
statusLabel.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
statusLabel.BackgroundTransparency = 1
statusLabel.Text = "Status: Not Working"
statusLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
statusLabel.TextScaled = true
statusLabel.Font = Enum.Font.SourceSans
statusLabel.Parent = frame
```

## ฟั่งชั่นรันสคริป
```lua
executeButton.MouseButton1Click:Connect(function()
    local scriptToRun = textBox.Text
    if scriptToRun ~= "" then
        local success, errorMsg = pcall(function()
            -- รันโค้ดจาก textBox ด้วย loadstring
            loadstring(scriptToRun)()
        end)
        
        if success then
            statusLabel.Text = "Status: Script Executed"
            statusLabel.TextColor3 = Color3.fromRGB(0, 255, 0)  -- เปลี่ยนสีเป็นเขียวเมื่อสำเร็จ
        else
            statusLabel.Text = "Status: Error - " .. errorMsg
            statusLabel.TextColor3 = Color3.fromRGB(255, 0, 0)  -- เปลี่ยนสีเป็นแดงหากมีข้อผิดพลาด
        end
    else
        statusLabel.Text = "Status: No Script"
        statusLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
    end
end)
```

## ฟั่งชั่นปุ่มเปิดปิด
```lua
local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 30, 0, 30)
toggleButton.Position = UDim2.new(0.5, 120, 0.5, -160)  -- วางปุ่มไว้ที่ตำแหน่งที่ต้องการ
toggleButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
toggleButton.Text = "K"
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.TextScaled = true
toggleButton.Font = Enum.Font.SourceSansBold
toggleButton.Parent = screenGui
```

## ขอบวงกลมปุ่มเปิดปิด
```lua
local toggleButtonCorner = Instance.new("UICorner")
toggleButtonCorner.CornerRadius = UDim.new(0, 15)
toggleButtonCorner.Parent = toggleButton
```

## ฟั่งชั่นเปิดปิด
```lua
local isVisible = true
toggleButton.MouseButton1Click:Connect(function()
    isVisible = not isVisible
    frame.Visible = isVisible
end)
```

## ฟั่งชั่นขยับปุ่ม
```lua
local dragging = true
local dragInput, dragStart, startPos

toggleButton.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = toggleButton.Position
    end
end)

toggleButton.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = input.Position - dragStart
        toggleButton.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

toggleButton.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
    end
end)
```

## ช่อง Dev YouTuber ZG hub
```lua
https://www.youtube.com/@robloxxcxc
```






