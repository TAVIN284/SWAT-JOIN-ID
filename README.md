local Players = game:GetService("Players")
local TeleportService = game:GetService("TeleportService")
local LocalPlayer = Players.LocalPlayer
local StarterGui = game:GetService("StarterGui")

-- Cria a GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "JobIDTeleportGUI"
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 350, 0, 150)
MainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
MainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
MainFrame.Parent = ScreenGui

local UICorner = Instance.new("UICorner", MainFrame)
UICorner.CornerRadius = UDim.new(0, 15)

local TitleLabel = Instance.new("TextLabel")
TitleLabel.Size = UDim2.new(1, 0, 0, 40)
TitleLabel.Position = UDim2.new(0, 0, 0, 0)
TitleLabel.Text = "Entrar por Job ID"
TitleLabel.TextColor3 = Color3.fromRGB(0, 255, 255)
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextSize = 22
TitleLabel.BackgroundTransparency = 1
TitleLabel.Parent = MainFrame

local JobIdBox = Instance.new("TextBox")
JobIdBox.Size = UDim2.new(0, 300, 0, 40)
JobIdBox.Position = UDim2.new(0, 25, 0, 50)
JobIdBox.PlaceholderText = "Coloque o Job ID aqui"
JobIdBox.Text = ""
JobIdBox.ClearTextOnFocus = false
JobIdBox.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
JobIdBox.TextColor3 = Color3.fromRGB(0, 255, 255)
JobIdBox.Font = Enum.Font.Gotham
JobIdBox.TextSize = 18
JobIdBox.Parent = MainFrame

local EnterButton = Instance.new("TextButton")
EnterButton.Size = UDim2.new(0, 100, 0, 40)
EnterButton.Position = UDim2.new(0.5, -50, 0, 100)
EnterButton.Text = "Entrar"
EnterButton.BackgroundColor3 = Color3.fromRGB(0, 210, 255)
EnterButton.TextColor3 = Color3.fromRGB(20, 20, 25)
EnterButton.Font = Enum.Font.GothamBold
EnterButton.TextSize = 22
EnterButton.Parent = MainFrame

local UICornerBtn = Instance.new("UICorner", EnterButton)
UICornerBtn.CornerRadius = UDim.new(0, 12)

-- Função para mostrar aviso
local function showMessage(msg)
    StarterGui:SetCore("SendNotification", {
        Title = "Job ID Teleport";
        Text = msg;
        Duration = 3;
    })
end

-- Função para entrar no servidor
EnterButton.MouseButton1Click:Connect(function()
    local jobId = JobIdBox.Text:gsub("%s+", "") -- remove espaços extras
    if jobId == "" then
        showMessage("Digite um Job ID válido!")
        return
    end

    local placeId = game.PlaceId
    showMessage("Tentando entrar no servidor...")

    local success, err = pcall(function()
        TeleportService:TeleportToPlaceInstance(placeId, jobId, LocalPlayer)
    end)

    if not success then
        showMessage("Falha ao entrar: " .. tostring(err))
    end
end)
