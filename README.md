# 🏦 Douglas Travel Finance - Agente Financeiro com MCP

> **Nota:** Este web app é uma demonstração de portfólio para o desafio da DIO. Todos os dados exibidos são fictícios.

## 🔗 Links do Projeto
- **Aplicação Publicada:** https://douglas-travel-wallet.lovable.app/
- **Repositório GitHub:**  https://github.com/dlocatelli7-hue/DouglasFinanceira/blob/main/README.md)

---

## 📌 Cenário Escolhido
O **Douglas Travel Finance** é um assistente financeiro pessoal integrado num contexto de agência/planeamento de viagens. Ele ajuda o utilizador a acompanhar saldos, contas e extratos categorizados (Alojamento, Transporte e Alimentação) durante as suas viagens.

---

## 🛠️ Configuração dos Servidores MCP
Configurados localmente no ambiente do VS Code via `mcp-config.json`:
- **Pluggy MCP:** Conectado via Streamable HTTP (`https://mcp.pluggy.ai/mcp`) para consultar especificações de documentação da API brasileira de Open Finance.
- **Plaid MCP:** Conectado via `uvx` / `stdio` no ambiente Sandbox, utilizando variáveis de ambiente (`PLAID_CLIENT_ID` e `PLAID_SECRET`) para simular dados bancários de teste.

---

## ⚙️ Regra de Negócio e Tratamento de Dados
Seguindo a convenção da API da Plaid, o tratamento de sinal no frontend foi padronizado através da seguinte função:

```typescript
function normalizeTransaction(amount: number, tipo: 'entrada' | 'saida') {
  const abs = Math.abs(amount);
  if (tipo === 'saida') {
    return abs;     // Saída / Gasto = Valor Positivo
  }
  return -abs;      // Entrada / Receita = Valor Negativo
}
