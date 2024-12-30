 Script de Auto-Farm para Blox Fruits - Black z 2
local player = game.Players.LocalPlayer

Função para farmar até o nível máximo
local function farmLevelMax()
    while player.Level < 2600 do -- Supondo que 2600 seja o nível máximo
        for _, npc in pairs(game.Workspace.Enemies:GetChildren()) do
            if npc:FindFirstChild("Humanoid") and npc.Humanoid.Health > 0 then
                player.Character.HumanoidRootPart.CFrame = npc.HumanoidRootPart.CFrame
                wait(0.5)
                game.ReplicatedStorage.Remotes.Combat:FireServer(npc)
            end
        end
        wait(1)
    end
    print("Nível máximo alcançado!")
end

-- Função para farmar Raids de Pirata
local function farmRaids()
    while true do
        local raidLocation = Vector3.new(100, 50, -75) -- Coordenadas de exemplo
        player.Character:MoveTo(raidLocation)
        wait(5)
        for _, enemy in pairs(game.Workspace.RaidEnemies:GetChildren()) do
            if enemy:FindFirstChild("Humanoid") and enemy.Humanoid.Health > 0 then
                player.Character.HumanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame
                wait(0.5)
                game.ReplicatedStorage.Remotes.Combat:FireServer(enemy)
            end
        end
        wait(10)
    end
end

-- Função para farmar maestria
local function farmMastery()
    while true do
        for _, npc in pairs(game.Workspace.Enemies:GetChildren()) do
            if npc:FindFirstChild("Humanoid") and npc.Humanoid.Health > 0 then
                player.Character.HumanoidRootPart.CFrame = npc.HumanoidRootPart.CFrame
                wait(0.5)
                game.ReplicatedStorage.Remotes.Combat:FireServer(npc)
            end
        end
        wait(1)
    end
end

-- Função para farmar God Human
local function farmGodHuman()
    while true do
        -- Código para farmar God Human
        -- Exemplo: atacar NPCs específicos para God Human
        for _, npc in pairs(game.Workspace.GodHumanEnemies:GetChildren()) do
            if npc:FindFirstChild("Humanoid") and npc.Humanoid.Health > 0 then
                player.Character.HumanoidRootPart.CFrame = npc.HumanoidRootPart.CFrame
                wait(0.5)
                game.ReplicatedStorage.Remotes.Combat:FireServer(npc)
            end
        end
        wait(1)
    end
end

-- Função para resgatar códigos automaticamente
local function redeemCodes()
    local codes = {"CODE1", "CODE2", "CODE3"} -- Substitua pelos códigos reais
    for _, code in pairs(codes) do
        game.ReplicatedStorage.Remotes.RedeemCode:InvokeServer(code)
        wait(1)
    end
end

-- Função para identificar o servidor
local function identifyServer()
    print("ID do servidor: " .. game.JobId)
end

-- Iniciar as funções de farm em threads separadas
spawn(farmLevelMax)
spawn(farmRaids)
spawn(farmMastery)
spawn(farmGodHuman)
spawn(redeemCodes)
identifyServer()


