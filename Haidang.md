-- dangdz
--[[ DANGDZ HUB - FIXED VERSION ]]
task.wait(0.5)
if _G.D then _G.D:Destroy() end
local s = Instance.new("ScreenGui", game:GetService("CoreGui"))
_G.D = s
local f = Instance.new("Frame", s)
f.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
f.Size = UDim2.new(0, 180, 0, 260)
f.Position = UDim2.new(0.5, -90, 0.5, -130)
f.Active, f.Draggable = true, true

local function b(t, p, c)
    local n = Instance.new("TextButton", f)
    n.Text, n.Size, n.Position = t, UDim2.new(0.9, 0, 0.12, 0), UDim2.new(0.05, 0, p, 0)
    n.BackgroundColor3, n.TextColor3 = Color3.fromRGB(45, 45, 45), Color3.new(1, 1, 1)
    n.MouseButton1Click:Connect(c)
end

local l = Instance.new("TextLabel", f)
l.Text, l.Size, l.BackgroundColor3, l.TextColor3 = "DANGDZ HUB (VIỆT)", UDim2.new(1, 0, 0.15, 0), Color3.fromRGB(0, 150, 0), Color3.new(1, 1, 1)

b("Auto Farm (Tu Danh)", 0.18, function()
    _G.F = not _G.F
    spawn(function()
        while _G.F do
            pcall(function()
                game:GetService("VirtualUser"):Button1Down(Vector2.new(0,1000))
            end)
            task.wait(0.1)
        end
    end)
end)

b("Auto Nhat Do (Bypass)", 0.32, function()
    _G.C = not _G.C
    spawn(function()
        while _G.C do
            pcall(function()
                for _, v in pairs(workspace:GetDescendants()) do
                    if v:IsA("Part") and (v.Name:find("Chest") or v:FindFirstChild("TouchTransmitter")) then
                        firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v, 0)
                        task.wait()
                        firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v, 1)
                    end
                end
            end)
            task.wait(1)
        end
    end)
end)

b("DONG MENU", 0.88, function() s:Destroy() _G.F, _G.C = false, false end)
