# Dangdz
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
l.Text, l.Size, l.BackgroundColor3, l.TextColor3 = "DANGDZ HUB (VIET)", UDim2.new(1, 0, 0.15, 0), Color3.fromRGB(0, 150, 0), Color3.new(1, 1, 1)

b("Auto Farm (Tu Danh)", 0.18, function()
_G.F = not _G.F
spawn(function()
while _G.F do
pcall(function()
local v = game:GetService("VirtualUser")
v:CaptureController()
v:Button1Down(Vector2.new(0,1000))
end)
task.wait(0.1)
end
end)
end)

b("Auto Ruong (Bypass)", 0.32, function()
_G.C = not _G.C
spawn(function()
while _G.C do
for _, v in pairs(game:GetService("Workspace"):GetDescendants()) do
if v:IsA("Part") and v.Name:find("Chest") then
local p = game.Players.LocalPlayer.Character.HumanoidRootPart
local d = (p.Position - v.Position).Magnitude
local t = game:GetService("TweenService"):Create(p, TweenInfo.new(d/150), {CFrame = v.CFrame})
t:Play() t.Completed:Wait()
firetouchinterest(p, v, 0) task.wait(0.1) firetouchinterest(p, v, 1)
end
end
task.wait(1)
end
end)
end)

b("Sieu Toc Do 100", 0.46, function()
_G.S = not _G.S
spawn(function()
while _G.S do
local c = game.Players.LocalPlayer.Character
if c and c:FindFirstChild("Humanoid") and c.Humanoid.MoveDirection.Magnitude > 0 then
c:TranslateBy(c.Humanoid.MoveDirection * 1.5)
end
task.wait()
end
end)
end)

b("Aimbot Ngam Dich", 0.60, function()
_G.A = not _G.A
spawn(function()
while _G.A do
local t, d = nil, 500
for _, v in pairs(game.Players:GetPlayers()) do
if v ~= game.Players.LocalPlayer and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
local p, o = workspace.CurrentCamera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
if o then
local m = (Vector2.new(p.X, p.Y) - Vector2.new(workspace.CurrentCamera.ViewportSize.X/2, workspace.CurrentCamera.ViewportSize.Y/2)).Magnitude
if m < d then t = v d = m end
end
end
end
if t then workspace.CurrentCamera.CFrame = CFrame.new(workspace.CurrentCamera.CFrame.Position, t.Character.HumanoidRootPart.Position) end
task.wait()
end
end)
end)

b("Nhay Cao + ESP", 0.74, function()
_G.J = true
game:GetService("UserInputService").JumpRequest:Connect(function() if _G.J then game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid"):ChangeState("Jumping") end end)
for _, p in pairs(game.Players:GetPlayers()) do
if p ~= game.Players.LocalPlayer and p.Character then
local h = Instance.new("Highlight", p.Character) h.FillColor = Color3.new(1, 0, 0)
end
end
end)

b("DONG MENU", 0.88, function() s:Destroy() _G.F, _G.C, _G.S, _G.A = false, false, false, false end)


