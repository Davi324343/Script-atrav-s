# Script-atrav-s
Hiii
local Players = game:GetService("Players")
local PhysicsService = game:GetService("PhysicsService")
local StarterGui = game:GetService("StarterGui")

local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Criar um grupo de colisão especial
PhysicsService:CreateCollisionGroup("NoCollide")
PhysicsService:CollisionGroupSetCollidable("NoCollide", "NoCollide", false)

-- Função para definir a colisão do personagem
local function setCollision(enable)
    for _, part in pairs(character:GetChildren()) do
        if part:IsA("BasePart") then
            part.CanCollide = enable
            part.CollisionGroupId = enable and 0 or PhysicsService:GetCollisionGroupId("NoCollide")
        end
    end
end

-- Criar interface gráfica
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = StarterGui

local function createButton(text, position, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 150, 0, 50)
    button.Position = position
    button.Text = text
    button.Parent = screenGui
    button.MouseButton1Click:Connect(callback)
end

-- Criar botões
createButton("Atravessar", UDim2.new(0.4, 0, 0.8, 0), function()
    setCollision(false)
end)

createButton("Parar", UDim2.new(0.6, 0, 0.8, 0), function()
    setCollision(true)
end)
