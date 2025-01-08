-- Carregando a biblioteca de UI
local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()

-- Criando a interface
local UI = Lib:Create{
    Theme = "Dark",
    Size = UDim2.new(0, 555, 0, 400)
}

local Main = UI:Tab{
    Name = "Inicia"
}

-- Divisores
local Divider = Main:Divider{
    Name = "Inicia shit"
}

local QuitDivider = Main:Divider{
    Name = "Sair"
}

-- Função "Kill all"
local KillAll = Divider:Button{
    Name = "Kill all",
    Description = "Kills all the players in the game!",
    Callback = function()
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character and player.Character:FindFirstChild("Humanoid") then
                player.Character.Humanoid.Health = 0  -- Mata o jogador
            end
        end
        print("All players killed.")
    end
}

-- Função de "Loop Kill all"
local LoopKillAll = Divider:Toggle{
    Name = "Loop kill all",
    Description = "Loop kills everyone in the game.",
    Callback = function(State)
        while State do
            for _, player in pairs(game.Players:GetPlayers()) do
                if player.Character and player.Character:FindFirstChild("Humanoid") then
                    player.Character.Humanoid.Health = 0  -- Mata o jogador
                end
            end
            wait(1)  -- Aguarda 1 segundo antes de matar novamente
        end
    end
}

-- Função de Teleportação
local TeleportLocation = Divider:Dropdown{
    Name = "Teleports",
    Options = {"Pleasant Park", "Loot Lake", "Tomato Town", "Wailing Woods", "Anarchy Acres", "Retail Row"},
    Callback = function(Value)
        local player = game.Players.LocalPlayer
        local teleportPositions = {
            ["Pleasant Park"] = Vector3.new(100, 10, 100),
            ["Loot Lake"] = Vector3.new(200, 10, 200),
            ["Tomato Town"] = Vector3.new(300, 10, 300),
            ["Wailing Woods"] = Vector3.new(400, 10, 400),
            ["Anarchy Acres"] = Vector3.new(500, 10, 500),
            ["Retail Row"] = Vector3.new(600, 10, 600)
        }
        
        if teleportPositions[Value] then
            player.Character:SetPrimaryPartCFrame(CFrame.new(teleportPositions[Value]))  -- Teleporta o jogador
            print("Teleported to: " .. Value)
        end
    end
}

-- Configuração da cor do ESP para verde
Divider:ColorPicker{
    Name = "ESP color",
    Default = Color3.fromRGB(0, 255, 0),  -- Verde
    Callback = function(Value)
        -- Configuração do ESP com a cor escolhida (já configurado para verde)
        print("ESP color changed to: ", Value)
    end
}

-- Função de "Box" (caixa de texto)
Divider:Box{
    Name = "Car name",
    ClearText = true,
    Callback = function(Value)
        print(Value)
    end
}

-- Função de "SearchDropdown" (busca de locais)
Divider:SearchDropdown{
    Name = "Teleports",
    Options = {"Pleasant Park", "Loot Lake", "Tomato Town", "Wailing Woods", "Anarchy Acres", "Retail Row"},
    ClearText = false,
    Callback = function(Value)
        print(Value)
    end
}

-- Botão para fechar a interface
local Quit = QuitDivider:Button{
    Name = "Closes the ui library.",
    Callback = function()
        UI:Quit{
            Message = "Fuck off...", -- mensagem de fechamento
            Length = 1 -- tempo que a mensagem aparece
        }
    end
}
