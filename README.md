-- [[ YEW AUTO PREMIUM - V3.8 整合版 ]]
local KEY_SECRET = "YEW-PRO-8829"
local ARGON_KEY_VALUE = "VswDjVBSVWQaSnqAPzyXvKmfZgyZkdcw" -- 你的 Luarmor Key
local DISCORD_LINK = "https://discord.gg/66AGb5Xvy"

local ScreenGui = Instance.new("ScreenGui", game:GetService("CoreGui"))
local Main = Instance.new("Frame", ScreenGui)
Main.Size = UDim2.new(0, 300, 0, 350) 
Main.Position = UDim2.new(0.5, -150, 0.5, -175)
Main.BackgroundColor3 = Color3.fromRGB(20, 20, 25)
Main.Active = true
Main.Draggable = true
Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 10)

local Title = Instance.new("TextLabel", Main)
Title.Text = "YEW AUTO - V3 LOGIN"
Title.Size = UDim2.new(1, 0, 0, 45)
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1
Title.Font = Enum.Font.GothamBold

-- [[ 登录面板 ]]
local Input = Instance.new("TextBox", Main)
Input.PlaceholderText = "输入 YEW 密钥..."
Input.Position = UDim2.new(0.1, 0, 0.15, 0)
Input.Size = UDim2.new(0.8, 0, 0, 35)
Input.BackgroundColor3 = Color3.fromRGB(35, 35, 40)
Input.TextColor3 = Color3.fromRGB(255, 255, 255)

local VerifyBtn = Instance.new("TextButton", Main)
VerifyBtn.Text = "登录 (Login)"
VerifyBtn.Position = UDim2.new(0.1, 0, 0.35, 0)
VerifyBtn.Size = UDim2.new(0.8, 0, 0, 40)
VerifyBtn.BackgroundColor3 = Color3.fromRGB(88, 101, 242)
VerifyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)

local BtnGetKey = Instance.new("TextButton", Main)
BtnGetKey.Text = "获取密钥 (Get Key)"
BtnGetKey.Position = UDim2.new(0.1, 0, 0.55, 0)
BtnGetKey.Size = UDim2.new(0.8, 0, 0, 40)
BtnGetKey.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
BtnGetKey.TextColor3 = Color3.fromRGB(255, 255, 255)

-- [[ 脚本按钮 ]]
local BtnWings = Instance.new("TextButton", Main)
BtnWings.Text = "加载 Wings Hub"
BtnWings.Position = UDim2.new(0.1, 0, 0.15, 0)
BtnWings.Size = UDim2.new(0.8, 0, 0, 40)
BtnWings.Visible = false

local BtnArgon = Instance.new("TextButton", Main)
BtnArgon.Text = "加载 Argon Hub"
BtnArgon.Position = UDim2.new(0.1, 0, 0.32, 0)
BtnArgon.Size = UDim2.new(0.8, 0, 0, 40)
BtnArgon.Visible = false

local BtnFPS = Instance.new("TextButton", Main)
BtnFPS.Text = "加载 Syrenix FPS"
BtnFPS.Position = UDim2.new(0.1, 0, 0.49, 0)
BtnFPS.Size = UDim2.new(0.8, 0, 0, 40)
BtnFPS.Visible = false

local BtnSpam = Instance.new("TextButton", Main)
BtnSpam.Text = "加载 YEW SPAM"
BtnSpam.Position = UDim2.new(0.1, 0, 0.66, 0)
BtnSpam.Size = UDim2.new(0.8, 0, 0, 40)
BtnSpam.Visible = false

for _, btn in pairs({BtnWings, BtnArgon, BtnFPS, BtnSpam}) do
    btn.BackgroundColor3 = Color3.fromRGB(45, 45, 50)
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Parent = Main
end

-- [[ 逻辑部分 ]]

BtnGetKey.MouseButton1Click:Connect(function()
    if setclipboard then setclipboard(DISCORD_LINK) end
    BtnGetKey.Text = "链接已复制！"
    task.wait(2)
    BtnGetKey.Text = "获取密钥 (Get Key)"
end)

VerifyBtn.MouseButton1Click:Connect(function()
    if Input.Text:gsub("%s+", "") == KEY_SECRET then
        VerifyBtn.Visible, Input.Visible, BtnGetKey.Visible = false, false, false
        Title.Text = "V3 - 选择功能"
        BtnWings.Visible, BtnArgon.Visible, BtnFPS.Visible, BtnSpam.Visible = true, true, true, true
    else
        VerifyBtn.Text = "密钥不匹配！"
        task.wait(1)
        VerifyBtn.Text = "登录 (Login)"
    end
end)

-- 1. Wings
BtnWings.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
    loadstring(game:HttpGet("https://wings.ac/loader"))()
end)

-- 2. Argon Hub (Luarmor 方式)
BtnArgon.MouseButton1Click:Connect(function()
    -- 自动复制 Key 到剪贴板以防万一
    if setclipboard then setclipboard(ARGON_KEY_VALUE) end
    ScreenGui:Destroy()
    
    -- 你要求的真正的 Luarmor 加载代码
    script_key = ARGON_KEY_VALUE
    loadstring(game:HttpGet("https://api.luarmor.net/files/v4/loaders/4109f8447808f89121335990a22ed888.lua"))()
end)

-- 3. Syrenix FPS
BtnFPS.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/FRAXXontop/Syrenixscriptz/refs/heads/main/SyrenixFPS.lua"))()
end)

-- 4. YEW SPAM
BtnSpam.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
    -- 这里保留你原始的 YEW SPAM Hook 代码逻辑
    local gui, frame, button = Instance.new("ScreenGui", game:GetService("CoreGui")), Instance.new("Frame"), Instance.new("TextButton")
    local stroke = Instance.new("UIStroke")
    gui.ResetOnSpawn = false
    frame.Size, frame.Position, frame.BackgroundColor3, frame.BorderSizePixel, frame.Active, frame.Draggable, frame.Parent = UDim2.new(0, 160, 0, 80), UDim2.new(0, 10, 0, 10), Color3.new(0, 0, 0), 0, true, true, gui
    stroke.Parent = frame
    stroke.Thickness = 3
    stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    button.Text, button.Size, button.Position, button.BackgroundColor3, button.BorderSizePixel, button.Font, button.TextColor3, button.TextSize, button.Parent = "YEW: 等待抓包", UDim2.new(1, -20, 1, -20), UDim2.new(0, 10, 0, 10), Color3.new(0, 0, 0), 0, Enum.Font.SourceSansBold, Color3.new(1, 1, 1), 16, frame
    task.spawn(function()
        local h = 0
        while task.wait(0.01) do
            h = h + 0.01
            if h > 1 then h = 0 end
            local col = Color3.fromHSV(h, 0.8, 1)
            stroke.Color = col
            button.TextColor3 = col
        end
    end)
    local activated = false
    local remote, f_raw = nil, nil
    local v1, v2, v3, v4, v5, v6, v7
    local isHooked = false
    local RunService = game:GetService("RunService")
    local function spamRemote()
        if remote and f_raw then f_raw(remote, v1, v2, v3, v4, v5, v6, v7) end
    end
    local function steppedSpam()
        for i = 1, 5 do
            task.spawn(function()
                while activated do
                    spamRemote()
                    RunService.Heartbeat:Wait()
                end
            end)
        end
    end
    local function toggleSpam()
        activated = not activated
        button.Text = activated and "STOP SPAM" or "START SPAM"
        if activated then steppedSpam() end
    end
    local function hookMetatable()
        local mt = getrawmetatable(game)
        local oldIndex = mt.__index
        setreadonly(mt, false)
        mt.__index = function(self, key)
            if key == "FireServer" then
                return function(obj, ...)
                    local a = {...}
                    if #a == 7 and typeof(a[4]) == "CFrame" then
                        remote = obj
                        f_raw = obj.FireServer
                        v1, v2, v3, v4, v5, v6, v7 = a[1], a[2], a[3], a[4], a[5], a[6], a[7]
                    end
                    return oldIndex(self, key)(obj, ...)
                end
            end
            return oldIndex(self, key)
        end
        setreadonly(mt, true)
        isHooked = true
    end
    button.MouseButton1Click:Connect(function()
        if not isHooked then hookMetatable() end
        toggleSpam()
    end)
end)

# V4-YEW-BLADE
Blade ball
