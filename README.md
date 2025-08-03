-- STUCK HUB - Mod Menu para Steal a Brainrot
-- Ícone com imagem personalizada para abrir/fechar o menu

-- Serviços Roblox
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TeleportService = game:GetService("TeleportService")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")

-- GUI Principal
local gui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
gui.Name = "Stuck_Hub"

-- Ícone de abrir/fechar com imagem personalizada
local toggleButton = Instance.new("ImageButton", gui)
toggleButton.Size = UDim2.new(0, 50, 0, 50)
toggleButton.Position = UDim2.new(0, 10, 0, 10)
toggleButton.BackgroundTransparency = 1
toggleButton.Image = "rbxassetid://**SEU_IMAGE_ID_AQUI**" -- 🔁 Substitua pelo ID da imagem

-- Menu principal
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 240, 0, 180)
frame.Position = UDim2.new(0.05, 0, 0.25, 0)
frame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
frame.BorderColor3 = Color3.fromRGB(255, 0, 0)
frame.BorderSizePixel = 2
frame.Visible = false
frame.Active = true
frame.Draggable = true
frame.Name = "StuckFrame"

-- Título
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 25)
title.Text = "STUCK HUB VIP+"
title.Font = Enum.Font.Code
title.TextSize = 18
title.TextColor3 = Color3.fromRGB(255, 0, 0)
title.BackgroundTransparency = 1

-- Subtítulo
local tiktok = Instance.new("TextLabel", frame)
tiktok.Size = UDim2.new(1, -10, 0, 20)
tiktok.Position = UDim2.new(0, 5, 0, 25)
tiktok.Text = "TIKTOK: @stuckhuboficial"
tiktok.Font = Enum.Font.Code
tiktok.TextSize = 14
tiktok.TextColor3 = Color3.fromRGB(255, 255, 255)
tiktok.BackgroundTransparency = 1

-- Criador de botões
local function createButton(text, posY, callback)
    local btn = Instance.new("TextButton", frame)
    btn.Size = UDim2.new(1, -10, 0, 30)
    btn.Position = UDim2.new(0, 5, 0, posY)
    btn.Text = text
    btn.Font = Enum.Font.Code
    btn.TextSize = 16
    btn.TextColor3 = Color3.fromRGB(255, 0, 0)
    btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    btn.MouseButton1Click:Connect(callback)
end

-- Super Jump
createButton("Super Jump", 50, function()
    local humanoid = Character:FindFirstChildWhichIsA("Humanoid")
    if humanoid then
        humanoid.UseJumpPower = true
        humanoid.JumpPower = 200
    end
end)

-- Fly para onde olha
local flying = false
createButton("Look Fly", 90, function()
    flying = not flying
    if flying then
        RunService:BindToRenderStep("StuckFly", Enum.RenderPriority.Input.Value, function()
            local cam = workspace.CurrentCamera
            HumanoidRootPart.Velocity = cam.CFrame.LookVector * 100
        end)
    else
        RunService:UnbindFromRenderStep("StuckFly")
    end
end)

-- Rejoin
createButton("Rejoin", 130, function()
    LocalPlayer:Kick("Reentrando...")
    wait(1)
    TeleportService:Teleport(game.PlaceId, LocalPlayer)
end)

-- Abrir / Fechar com imagem
toggleButton.MouseButton1Click:Connect(function()
    frame.Visible = not frame.Visible
end)
