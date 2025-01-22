local Players = game:GetService("Players")
local player = Players.LocalPlayer
local gui = player:WaitForChild("PlayerGui")

-- Criar botões móveis na tela
local function criarBotao(nome, posicao, funcao)
    local botao = Instance.new("TextButton")
    botao.Name = nome
    botao.Size = UDim2.new(0, 100, 0, 50)
    botao.Position = posicao
    botao.Text = nome
    botao.Parent = gui
    botao.MouseButton1Click:Connect(funcao)
    return botao
end

-- Função para mostrar a localização dos jogadores
local function mostrarLocalizacao()
    while true do
        for _, jogador in pairs(Players:GetPlayers()) do
            if jogador ~= player then
                print(jogador.Name .. " está em: " .. tostring(jogador.Character.PrimaryPart.Position))
            end
        end
        wait(5) -- Atualiza a cada 5 segundos
    end
end

-- Função para garantir estamina infinita
local function estaminaInfinita()
    while true do
        player.Character.Humanoid.WalkSpeed = 50 -- Ajuste o valor conforme necessário
        wait(1)
    end
end

-- Função para ativar/desativar localização
local localizacaoAtiva = false
local function toggleLocalizacao()
    localizacaoAtiva = not localizacaoAtiva
    if localizacaoAtiva then
        coroutine.wrap(mostrarLocalizacao)()
    end
end

-- Função para ativar/desativar estamina infinita
local estaminaAtiva = false
local function toggleEstamina()
    estaminaAtiva = not estaminaAtiva
    if estaminaAtiva then
        coroutine.wrap(estaminaInfinita)()
    end
end

-- Criar os botões na tela
local botaoLocalizacao = criarBotao("Toggle Localização", UDim2.new(0, 50, 0, 50), toggleLocalizacao)
local botaoEstamina = criarBotao("Toggle Estamina", UDim2.new(0, 50, 0, 110), toggleEstamina)
