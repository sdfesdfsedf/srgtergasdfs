getgenv().settings = {
    key = "Q",
    part = "HumanoidRootPart",
    smoothness = 1,
    prediction = Vector3.new(.11945, 0.11, 0.11934)
}

local Plr = nil
local IsTargetting = false

local CC = workspace.CurrentCamera
local Mouse = game.Players.LocalPlayer:GetMouse()

Mouse.KeyDown:Connect(function(Key)
    local Keybind = getgenv().settings.key:lower()
    if (Key == Keybind) then
        IsTargetting = not IsTargetting
        if IsTargetting then
            Plr = GetClosest()
        else
            if Plr ~= nil then
                Plr = nil
            end
        end
    end
end)

function GetClosest()
    local closestPlayer
    local shortestDistance = math.huge
    for i, v in pairs(game.Players:GetPlayers()) do
        pcall(function()
            if v ~= game.Players.LocalPlayer and v.Character and
                v.Character:FindFirstChild("Humanoid") then
                local pos = CC:WorldToViewportPoint(v.Character.PrimaryPart.Position)
                local magnitude = (Vector2.new(pos.X, pos.Y) - Vector2.new(Mouse.X, Mouse.Y)).magnitude
                if magnitude < shortestDistance then
                    closestPlayer = v
                    shortestDistance = magnitude
                end
            end
        end)
    end
    return closestPlayer
end

local aimbot = true

function Aimbot()
    if aimbot == true and Plr ~= nil then
        local Main = CFrame.new(CC.CFrame.p, Plr.Character[getgenv().settings.part].Position + (Plr.Character[getgenv().settings.part].Velocity * getgenv().settings.prediction))
        CC.CFrame = CC.CFrame:Lerp(Main, getgenv().settings.smoothness)
    end
end



game.RunService.Heartbeat:Connect(Aimbot)

for _, con in next, getconnections(workspace.CurrentCamera.Changed) do
    con:Disable()
end

for _, con in next, getconnections(workspace.CurrentCamera:GetPropertyChangedSignal("CFrame")) do
    con:Disable()
end
