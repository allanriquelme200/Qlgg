-- Configurações iniciais
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humRoot = character:WaitForChild("HumanoidRootPart")
local hum = character:WaitForChild("Humanoid")

-- Função para caminhar até um ponto específico
local function walkToPosition(targetPosition)
    hum:MoveTo(targetPosition)
end

-- Função para pegar o saco de lixo
local function pickUpTrash()
    -- Localiza o objeto "Saco de lixo"
    local trashObject = workspace:FindFirstChild("Saco de lixo")
    if trashObject then
        -- Simula o clique para pegar o lixo
        fireclickdetector(trashObject:FindFirstChildOfClass("ClickDetector"))
    end
end

-- Função para entregar o lixo
local function deliverTrash()
    -- Localiza o NPC ou objeto de entrega de lixo
    local deliveryNPC = workspace:FindFirstChild("Entregar lixo")
    if deliveryNPC then
        -- Simula o clique para entregar o lixo
        fireclickdetector(deliveryNPC:FindFirstChildOfClass("ClickDetector"))
    end
end

-- Loop principal do auto farm
while true do
    -- Caminha até o local do lixo
    walkToPosition(workspace["Saco de lixo"].Position)

    -- Espera chegar ao local do lixo
    repeat wait() until (humRoot.Position - workspace["Saco de lixo"].Position).Magnitude < 5

    -- Pega o saco de lixo
    pickUpTrash()

    -- Caminha até o NPC de entrega
    walkToPosition(workspace["Entregar lixo"].Position)

    -- Espera chegar ao NPC de entrega
    repeat wait() until (humRoot.Position - workspace["Entregar lixo"].Position).Magnitude < 5

    -- Entrega o lixo
    deliverTrash()

    -- Aguarda um pouco antes de repetir o ciclo
    wait(2) -- Ajuste esse tempo conforme necessário
end
