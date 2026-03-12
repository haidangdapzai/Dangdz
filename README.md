--[[
    DZ HUB - BLOX FRUITS EDITION
    Created by: Hai Dang
]]

-- Chờ game load
repeat wait() until game:IsLoaded() and game.Players.LocalPlayer

-- Khởi tạo Rayfield UI
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "🦖 DZ Hub | Blox Fruits 🌸",
   LoadingTitle = "Đang nạp DZ Hub...",
   LoadingSubtitle = "by Hai Dang",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "DZ_Hub_Config",
      FileName = "MainConfig"
   }
})

-- Biến toàn cục (Settings)
getgenv().Setting = {
    ["AutoAim"] = { ["Enable"] = false, ["Distance"] = 1000 },
    ["Team"] = "Pirates",
    ["Skip"] = { ["FruitList"] = {"Buddha", "Leopard", "T-Rex"} }
}

-- Tab Chính
local MainTab = Window:CreateTab("Tự động săn", 4483362458)

local Section = MainTab:CreateSection("Cấu hình Bounty")

MainTab:CreateToggle({
   Name = "Bật Auto Bounty (SynTrax)",
   CurrentValue = false,
   Callback = function(Value)
      if Value then
          loadstring(game:HttpGet("https://raw.githubusercontent.com/DevHub-roblox/script-SYNTRAX-Hub/refs/heads/main/SynTrax-Auto-bounty"))()
      end
   end,
})

-- Tab Chiến đấu
local CombatTab = Window:CreateTab("Chiến đấu", 4483362458)

CombatTab:CreateToggle({
   Name = "Auto Aim (T�� khóa mục tiêu)",
   CurrentValue = false,
   Callback = function(Value)
      getgenv().Setting["AutoAim"]["Enable"] = Value
   end,
})

CombatTab:CreateSlider({
   Name = "Khoảng cách Aim",
   Min = 100,
   Max = 3000,
   Default = 1000,
   Color = Color3.fromRGB(255, 255, 255),
   Increment = 100,
   ValueName = "Khoảng cách",
   Callback = function(Value)
      getgenv().Setting["AutoAim"]["Distance"] = Value
   end,
})

-- Logic Auto Aim chạy ngầm
local Camera = workspace.CurrentCamera
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- Verify LocalPlayer has character before spawning auto aim task
if LocalPlayer.Character then
    task.spawn(function()
        while task.wait(0.1) do
            if getgenv().Setting["AutoAim"]["Enable"] then
                local target = nil
                local dist = getgenv().Setting["AutoAim"]["Distance"]
                
                for _, v in pairs(Players:GetPlayers()) do
                    if v ~= LocalPlayer and v.Character and v.Character:FindFirstChild("HumanoidRootPart") and v.Character:FindFirstChild("Humanoid") then
                        local humanoid = v.Character.Humanoid
                        if humanoid.Health > 0 then
                            local magnitude = (v.Character.HumanoidRootPart.Position - LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
                            if magnitude < dist then
                                dist = magnitude
                                target = v
                            end
                        end
                    end
                end
                
                if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
                    Camera.CFrame = CFrame.new(Camera.CFrame.Position, target.Character.HumanoidRootPart.Position)
                end
            end
        end
    end)
end

Rayfield:Notify({
   Title = "DZ Hub Đã Sẵn Sàng!",
   Content = "Chào mừng bạn trở lại, Hai Dang! 🦖🌸",
   Duration = 5,
   Image = 4483362458,
})
