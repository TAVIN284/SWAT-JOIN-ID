loadstring([[
local a=game:GetService("Players").LocalPlayer
local b=game:GetService("TeleportService")
local c=game:GetService("StarterGui")
local d=Instance.new("ScreenGui",a:WaitForChild("PlayerGui"))
d.Name="JobIDTeleportGUI"
local e=Instance.new("Frame",d)
e.Size=UDim2.new(0,350,0,150)
e.Position=UDim2.new(0.5,0,0.5,0)
e.AnchorPoint=Vector2.new(0.5,0.5)
e.BackgroundColor3=Color3.fromRGB(30,30,40)
Instance.new("UICorner",e).CornerRadius=UDim.new(0,15)
local f=Instance.new("TextLabel",e)
f.Size=UDim2.new(1,0,0,40)
f.Position=UDim2.new(0,0,0,0)
f.Text="Entrar por Job ID"
f.TextColor3=Color3.fromRGB(0,255,255)
f.Font=Enum.Font.GothamBold
f.TextSize=22
f.BackgroundTransparency=1
local g=Instance.new("TextBox",e)
g.Size=UDim2.new(0,300,0,40)
g.Position=UDim2.new(0,25,0,50)
g.PlaceholderText="Coloque o Job ID aqui"
g.Text=""
g.ClearTextOnFocus=false
g.BackgroundColor3=Color3.fromRGB(50,50,60)
g.TextColor3=Color3.fromRGB(0,255,255)
g.Font=Enum.Font.Gotham
g.TextSize=18
local h=Instance.new("TextButton",e)
h.Size=UDim2.new(0,100,0,40)
h.Position=UDim2.new(0.5,-50,0,100)
h.Text="Entrar"
h.BackgroundColor3=Color3.fromRGB(0,210,255)
h.TextColor3=Color3.fromRGB(20,20,25)
h.Font=Enum.Font.GothamBold
h.TextSize=22
Instance.new("UICorner",h).CornerRadius=UDim.new(0,12)
local function i(j)local k={Title="Job ID Teleport",Text=j,Duration=3}c:SetCore("SendNotification",k)end
h.MouseButton1Click:Connect(function()
local l=g.Text:gsub("%s+","")
if l==""then i("Digite um Job ID válido!")return end
local m=game.PlaceId
i("Tentando entrar no servidor...")
local n,o=pcall(function()b:TeleportToPlaceInstance(m,l,a)end)
if not n then i("Falha ao entrar: "..tostring(o))end
end)
]])()
