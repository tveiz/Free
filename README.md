local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

-- Criando a Janela da Interface
local Window = Rayfield:CreateWindow({
    Name = "Mini Hub Free😈",
    LoadingTitle = "Mini Hub free",
    LoadingSubtitle = "by Thziin",
    ConfigurationSaving = {
        Enabled = false
    }
})

local rev = Window:CreateTab("Revistar")
local Paragraph = rev:CreateParagraph({Title = "MINI HUB ON TOPPP", Content = "Feito por Th"})
local Section = rev:CreateSection("NECESSARIO")
local Button = rev:CreateButton({
   Name = "Roubar inv",
   Callback = function()
      local function deletarNotifyGui()
         local playerGui = game.Players.LocalPlayer:WaitForChild("PlayerGui")
         for _, gui in ipairs(playerGui:GetChildren()) do
            if gui.Name == "NotifyGui" and gui:IsA("ScreenGui") then
               gui:Destroy()
            end
         end
      end

      local itens = {"AK47", "Uzi", "Parafal", "Faca", "IA2", "G3", "Escudo", "C4", "AR-15", "Hi Power", "Natalina"}
      local args = { [1] = "mudaInv", [2] = "2", [4] = "1" }

      while true do
         deletarNotifyGui()
         for i, item in ipairs(itens) do
            if i <= 16 then
               args[3] = item
               args[2] = tostring(i)
               task.spawn(function()
                  game:GetService("ReplicatedStorage"):WaitForChild("Modules"):WaitForChild("InvRemotes"):WaitForChild("InvRequest"):InvokeServer(unpack(args))
               end)
            end
         end
         wait(0)
      end
   end,
})

rev:CreateSection("PC")
rev:CreateToggle({
   Name = "mandar revistar (TECLA E)",
   CurrentValue = false,
   Flag = "rvst",
   Callback = function(Value)
       getgenv().Enabled = Value
   end,
})

rev:CreateSection("MOBILE")
rev:CreateButton({
   Name = "mandar revistar UI",
   Callback = function()
      local TextChatService = game:GetService("TextChatService")
      local function sendRevistarMessage()
         local channel = TextChatService:WaitForChild("TextChannels"):WaitForChild("RBXGeneral")
         channel:SendAsync("/revistar morto")
      end

      local ScreenGui = Instance.new("ScreenGui")
      local Frame = Instance.new("Frame")
      local CloseButton = Instance.new("TextButton")
      local RevistarButton = Instance.new("TextButton")
      local Title = Instance.new("TextLabel")

      ScreenGui.Name = "RevistarUI"
      ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

      Frame.Size = UDim2.new(0, 300, 0, 150)
      Frame.Position = UDim2.new(0.5, -150, 0.5, -75)
      Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
      Frame.BorderSizePixel = 0
      Frame.BackgroundTransparency = 0.1
      Frame.Active = true
      Frame.Draggable = true

      Title.Size = UDim2.new(1, 0, 0, 30)
      Title.Position = UDim2.new(0, 0, 0, 0)
      Title.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
      Title.Text = "Mini Hub😈"
      Title.TextColor3 = Color3.fromRGB(255, 255, 255)
      Title.Font = Enum.Font.SourceSansBold
      Title.TextSize = 18

      CloseButton.Size = UDim2.new(0, 30, 0, 30)
      CloseButton.Position = UDim2.new(1, -30, 0, 0)
      CloseButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
      CloseButton.Text = "X"
      CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
      CloseButton.Font = Enum.Font.SourceSansBold
      CloseButton.TextSize = 18
      CloseButton.MouseButton1Click:Connect(function()
         ScreenGui:Destroy()
      end)

      RevistarButton.Size = UDim2.new(0.8, 0, 0.4, 0)
      RevistarButton.Position = UDim2.new(0.1, 0, 0.5, -30)
      RevistarButton.BackgroundColor3 = Color3.fromRGB(50, 150, 250)
      RevistarButton.Text = "manda /revistar morto"
      RevistarButton.TextColor3 = Color3.fromRGB(255, 255, 255)
      RevistarButton.Font = Enum.Font.SourceSansBold
      RevistarButton.TextSize = 20
      RevistarButton.AutoButtonColor = true
      RevistarButton.MouseButton1Click:Connect(function()
         sendRevistarMessage()
      end)

      Frame.Parent = ScreenGui
      Title.Parent = Frame
      CloseButton.Parent = Frame
      RevistarButton.Parent = Frame
   end,
})

rev:CreateSection("Anti Revistar")
rev:CreateToggle({
   Name = "Anti ser revistado",
   CurrentValue = false,
   Flag = "antirevistar",
   Callback = function(Value)
      if Value then
         local player = game.Players.LocalPlayer
         local character = player.Character or player.CharacterAdded:Wait()
         local humanoid = character:WaitForChild("Humanoid")

         humanoid.HealthChanged:Connect(function(health)
            if health <= 5 then
               player:Kick("ANTI SER REVISTADO")
            end
         end)
      end
   end,
})

rev:CreateSection("ESP")
local Players = game:GetService("Players")
local ESPAtivo = false

local function removerESP(player)
    if player.Character and player.Character:FindFirstChild("Head") then
        local head = player.Character.Head
        local esp = head:FindFirstChild("ESP")
        if esp then
            esp:Destroy()
        end
    end
end

local function criarESP(player)
    if player.Character and player.Character:FindFirstChild("Head") then
        if player.Character.Head:FindFirstChild("ESP") then return end

        local billboard = Instance.new("BillboardGui")
        billboard.Name = "ESP"
        billboard.Adornee = player.Character.Head
        billboard.AlwaysOnTop = true
        billboard.Size = UDim2.new(0, 200, 0, 50)
        billboard.StudsOffset = Vector3.new(0, 2, 0)

        local nameLabel = Instance.new("TextLabel")
        nameLabel.Size = UDim2.new(1, 0, 0.5, 0)
        nameLabel.Position = UDim2.new(0, 0, 0, 0)
        nameLabel.BackgroundTransparency = 1
        nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        nameLabel.TextStrokeTransparency = 0.5
        nameLabel.TextScaled = true
        nameLabel.Text = player.Name
        nameLabel.Parent = billboard

        local healthLabel = Instance.new("TextLabel")
        healthLabel.Size = UDim2.new(1, 0, 0.5, 0)
        healthLabel.Position = UDim2.new(0, 0, 0.5, 0)
        healthLabel.BackgroundTransparency = 1
        healthLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
        healthLabel.TextStrokeTransparency = 0.5
        healthLabel.TextScaled = true
        healthLabel.Text = "Vida: ..."
        healthLabel.Parent = billboard

        billboard.Parent = player.Character.Head

        local function atualizarVida()
            if player.Character and player.Character:FindFirstChild("Humanoid") then
                healthLabel.Text = "Vida: " .. math.floor(player.Character.Humanoid.Health)
            end
        end

        atualizarVida()
        player.Character:FindFirstChild("Humanoid").HealthChanged:Connect(atualizarVida)
    end
end

local function aplicarESP()
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= Players.LocalPlayer then
            if player.Character then criarESP(player) end
            player.CharacterAdded:Connect(function()
                wait(1)
                if ESPAtivo then criarESP(player) end
            end)
        end
    end

    Players.PlayerAdded:Connect(function(player)
        player.CharacterAdded:Connect(function()
            wait(1)
            if ESPAtivo then criarESP(player) end
        end)
    end)
end

rev:CreateToggle({
    Name = "ESP nome/vida",
    CurrentValue = false,
    Flag = "esp",
    Callback = function(Value)
        ESPAtivo = Value
        if Value then
            aplicarESP()
        else
            for _, player in pairs(Players:GetPlayers()) do
                removerESP(player)
            end
        end
    end,
})
