# 🔄 GitHub MCP Server com Claude Desktop

Este guia explica como configurar o servidor MCP oficial do GitHub para uso com o Claude Desktop, permitindo que você interaja com seus repositórios GitHub através do Claude.

Este repositório também inclui um arquivo de exemplo na raiz do projeto que demonstra casos de uso comuns.

## 📋 Requisitos 

1. **[Claude Desktop](https://claude.ai/download)** instalado e atualizado
2. **Node.js e npm** instalados no seu computador
3. **Token de Acesso Pessoal do GitHub** (você criará isso durante o processo)
4. Opcionalmente: **Docker** para execução em contêiner

## 🔑 Passo 1: Criar um Token de Acesso Pessoal do GitHub

1. Acesse [github.com](https://github.com) e faça login na sua conta
2. Clique em seu avatar no canto superior direito e selecione **Settings**
3. No menu lateral, selecione **Developer settings**
4. Clique em **Personal access tokens** e depois em **Generate new token**
5. Dê um nome descritivo como "Claude MCP Server"
6. Selecione as permissões necessárias:
   - Para acesso total a repositórios privados, selecione `repo`
   - Para acesso apenas a repositórios públicos, selecione `public_repo`
7. Clique em **Generate token**
8. **IMPORTANTE**: Copie e guarde o token gerado em local seguro, pois ele não será mostrado novamente

## ⚙️ Passo 2: Configurar o Claude Desktop

### Opção A: Usando Docker (Recomendado)

1. Abra o menu do Claude Desktop e selecione **Settings**
2. No painel de configurações, clique em **Developer** no menu lateral
3. Clique em **Edit Config**
4. Adicione o seguinte JSON ao arquivo de configuração, substituindo `<YOUR_TOKEN>` pelo seu token do GitHub:

```json
{
  "mcpServers": {
    "github": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GITHUB_PERSONAL_ACCESS_TOKEN",
        "ghcr.io/github/github-mcp-server"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

### Opção B: Usando NPX (Sem Docker)

1. Abra o menu do Claude Desktop e selecione **Settings**
2. No painel de configurações, clique em **Developer** no menu lateral
3. Clique em **Edit Config**
4. Adicione o seguinte JSON ao arquivo de configuração, substituindo `<YOUR_TOKEN>` pelo seu token do GitHub:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

> **Nota**: NPX é uma ferramenta incluída com o Node.js que permite executar pacotes sem instalá-los permanentemente. Esta opção é ideal para usuários que não têm Docker instalado ou preferem uma configuração mais leve.

## 📁 Passo 3: Localização do arquivo de configuração

O arquivo de configuração está localizado em:

- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `C:\Users\[SeuUsuário]\AppData\Roaming\Claude\claude_desktop_config.json` ou `C:\Users\[SeuUsuário]\AppData\Local\AnthropicClaude\claude_desktop_config.json`

Se o arquivo não existir, crie-o.

## 🔄 Passo 4: Reiniciar o Claude Desktop

1. Salve o arquivo de configuração
2. Feche completamente o Claude Desktop (certifique-se de que não está rodando em segundo plano)
3. Abra o Claude Desktop novamente

## ✅ Passo 5: Verificar a integração

1. No Claude Desktop, inicie uma nova conversa
2. Você deve ver um ícone de ferramentas (martelo) no canto inferior direito da caixa de entrada
3. Clique neste ícone para ver as ferramentas GitHub disponíveis
4. Teste a integração pedindo ao Claude para realizar uma operação simples do GitHub, como listar seus repositórios

## 📝 Exemplos de Uso

Na raiz deste repositório você encontrará um arquivo de exemplo ([exemplo-de-uso.md](./exemplo-de-uso.md)) que demonstra como utilizar a integração do GitHub com o Claude Desktop em cenários práticos. Consulte este arquivo para:

- Ver exemplos de comandos e solicitações para o Claude
- Entender os fluxos de trabalho comuns para gerenciamento de código
- Aprender a usar recursos avançados da integração

## 🔧 Resolução de Problemas

### Ativar o Modo Desenvolvedor

1. No Claude Desktop, vá para o menu (geralmente representado por três linhas ou pontos) -> **Help** -> **Enable Developer Mode**
2. No menu **Developer**, você pode abrir o arquivo de log MCP para obter informações detalhadas sobre as conexões do servidor

### Verificar Caminhos

- Certifique-se de que todos os caminhos no arquivo `claude_desktop_config.json` estão corretos
- No Windows, use barras duplas (`\\`) nos caminhos

### Testar Servidores Individualmente

Em um terminal como administrador, tente executar o servidor manualmente:

```bash
# Para o servidor GitHub usando NPX
npx -y @modelcontextprotocol/server-github
```

### Problemas Comuns no Windows

- Execute o Claude Desktop como administrador
- Use caminhos absolutos para executáveis e arquivos
- Instale globalmente os pacotes MCP (`npm install -g @modelcontextprotocol/server-github`)
- Verifique se as variáveis de ambiente estão configuradas corretamente

## 📚 Recursos Adicionais

- [Documentação oficial do MCP](https://modelcontextprotocol.io/)
- [GitHub do servidor MCP do GitHub](https://github.com/github/github-mcp-server)
- [Repositório de servidores MCP](https://github.com/modelcontextprotocol/servers)
