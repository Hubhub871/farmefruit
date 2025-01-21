-- Função para verificar a presença de frutas
local function verificarFrutas()
    local frutas = workspace:FindPartsInRegion3(workspace.CurrentCamera.CFrame.Position, Vector3.new(100, 100, 100), nil)
    local frutasEncontradas = false

    -- Loop para procurar as frutas
    for _, item in ipairs(frutas) do
        if item.Name == "Fruit" then
            frutasEncontradas = true
            break
        end
    end

    return frutasEncontradas
end

-- Função para avisar o jogador caso não haja frutas
local function avisarMudarDeServidor()
    if not verificarFrutas() then
        -- Mensagem para o jogador sobre a falta de frutas
        game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer("Não há frutas no servidor! Considere mudar de servidor.", "All")
    end
end

-- Verificar a presença de frutas a cada 30 segundos
while true do
    avisarMudarDeServidor()
    wait(30) -- Espera 30 segundos para verificar novamente
end
