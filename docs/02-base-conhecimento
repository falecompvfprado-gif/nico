# Base de Conhecimento: Nico - Seu Guia de Bolso

## Dados Utilizados

O Nico baseia suas interações e explicações didáticas em quatro conjuntos de dados principais estruturados no diretório `data/`:

|**Arquivo**|**Formato**|**Para que serve no Nico?**|
|---|---|---|
|`historico_atendimento.csv`|CSV|Resgatar interações e dúvidas passadas do cliente para dar continuidade ao aprendizado sem que ele precise repetir tudo.|
|`perfil_investidor.json`|JSON|Compreender a tolerância a risco, metas de vida, idade e progresso da reserva financeira para contextualizar e personalizar os exemplos teóricos.|
|`produtos_financeiros.json`|JSON|Funcionar como a "grade curricular" do Nico, contendo os detalhes técnicos de taxas, riscos e prazos dos produtos que ele é capaz de ensinar.|
|`transacoes.csv`|CSV|Analisar o fluxo de entradas e saídas do cliente para puxar dados reais de gastos como exemplos práticos na hora de explicar conceitos de orçamento.|

## Adaptações nos Dados

Para garantir que o Nico ensine conceitos financeiros de forma segura e fácil de validar, as seguintes adaptações foram feitas na base de dados original:

1. **Substituição de Ativos Complexos (Fundo Multimercado por FIIs):** O Fundo de Investimento Imobiliário (FII) substituiu o Fundo Multimercado. Como os FIIs são amplamente conhecidos por distribuir proventos mensais (dividendos), o Nico consegue usar esse conceito prático para explicar de forma lúdica a diferença entre ganho de capital e geração de renda passiva recorrente.
    
2. **Simplificação de Rentabilidades:** As descrições de rentabilidade dos produtos de renda fixa foram padronizadas para facilitar o cálculo aproximado em tempo real e evitar confusões matemáticas geradas por taxas indicativas flutuantes.
    

## Estratégia de Integração

### Como os dados são carregados?

O agente interage com os arquivos de dados locais em Python. Durante a inicialização da aplicação em Streamlit, um script lê os arquivos estruturados e armazena os dados em memória:

Python

```
perfil = json.load(open('./data/perfil_investidor.json'))
transacoes = pd.read_csv('./data/transacoes.csv')
historico = pd.read_csv('./data/historico_atendimento.csv')
produtos = json.load(open('./data/produtos_financeiros.json'))
```

### Como os dados são usados no prompt?

Para garantir o comportamento mais inteligente possível do Nico, os dados estruturados são sintetizados e acoplados dinamicamente no prompt do sistema (_system prompt_) ou injetados na memória de contexto a cada turno de conversa.

- **Dados Estáticos de Apoio (Produtos):** São injetados como referências fixas no prompt para que o Nico explique apenas o portfólio didático autorizado.
    
- **Dados Dinâmicos do Usuário (Perfil e Transações):** São processados e formatados de maneira amigável antes de serem enviados à LLM, evitando sobrecarregar o contexto com dados brutos desnecessários.
    

Plaintext

```
DADOS DO CLIENTE E PERFIL (data/perfil_investidor.json):
{
  "nome": "João Silva",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}

TRANSACOES DO CLIENTE (data/transacoes.csv):
data,descricao,categoria,valor,tipo
2025-10-01,Salário,receita,5000.00,entrada
2025-10-02,Aluguel,moradia,1200.00,saida
2025-10-03,Supermercado,alimentacao,450.00,saida
2025-10-05,Netflix,lazer,55.90,saida
2025-10-07,Farmácia,saude,89.00,saida
2025-10-10,Restaurante,alimentacao,120.00,saida
2025-10-12,Uber,transporte,45.00,saida
2025-10-15,Conta de Luz,moradia,180.00,saida
2025-10-20,Academia,saude,99.00,saida
2025-10-25,Combustível,transporte,250.00,saida

HISTORICO DE ATENDIMENTO DO CLIENTE (data/historico_atendimento.csv):
data,canal,tema,resumo,resolvido
2025-09-15,chat,CDB,Cliente perguntou sobre rentabilidade e prazos,sim
2025-09-22,telefone,Problema no app,Erro ao visualizar extrato foi corrigido,sim
2025-10-01,chat,Tesouro Selic,Cliente pediu explicação sobre o funcionamento do Tesouro Direto,sim
2025-10-12,chat,Metas financeiras,Cliente acompanhou o progresso da reserva de emergência,sim
2025-10-25,email,Atualização cadastral,Cliente atualizou e-mail e telefone,sim

PRODUTOS DISPONIVEIS PARA ENSINO (data/produtos_financeiros.json):
[
  {
    "nome": "Tesouro Selic",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "100% da Selic",
    "aporte_minimo": 30.00,
    "indicado_para": "Reserva de emergência e iniciantes"
  },
  {
    "nome": "CDB Liquidez Diária",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "102% do CDI",
    "aporte_minimo": 100.00,
    "indicado_para": "Quem busca segurança com rendimento diário"
  },
  {
    "nome": "LCI/LCA",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "95% do CDI",
    "aporte_minimo": 1000.00,
    "indicado_para": "Quem pode esperar 90 dias (isento de IR)"
  },
  {
    "nome": "Fundo Imobiliário (FII)",
    "categoria": "fundo",
    "risco": "medio",
    "rentabilidade": "Dividend Yield (DY) costuma ficar entre 6% a 12% ao ano",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil moderado que busca diversificação e renda recorrente mensal"
  },
  {
    "nome": "Fundo de Ações",
    "categoria": "fundo",
    "risco": "alto",
    "rentabilidade": "Variável",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil arrojado com foco no longo prazo"
  }
]
```

## Exemplo de Contexto Montado

Sempre que o usuário fizer uma pergunta, o Nico receberá uma versão resumida e limpa para evitar consumo excessivo de tokens, mantendo apenas o essencial para a criação de exemplos didáticos enriquecedores:

```
DADOS DO CLIENTE ATUAL:
- Nome: João Silva
- Perfil de Investidor: Moderado
- Objetivo Principal: Construir reserva de emergência
- Progresso Financeiro: Possui R$ 10.000 de uma meta de R$ 15.000 para emergências
  
HISTÓRICO DO MÊS ATUAL (SAÍDAS CONSOLIDADAS):
- Moradia: R$ 1.380 (Aluguel: R$ 1.200 + Luz: R$ 180)
- Alimentação: R$ 570 (Supermercado: R$ 450 + Restaurante: R$ 120)
- Transporte: R$ 295 (Uber: R$ 45 + Combustível: R$ 250)
- Saúde: R$ 188 (Farmácia: R$ 89 + Academia: R$ 99)
- Lazer: R$ 55,90 (Netflix)
- Total Gasto: R$ 2.488,90

MENU DE PRODUTOS DISPONÍVEIS PARA EXPLICAÇÃO DIDÁTICA:
1. Tesouro Selic (Renda Fixa / Baixo Risco / Mínimo R$ 30,00)
2. CDB Liquidez Diária (Renda Fixa / Baixo Risco / Mínimo R$ 100,00)
3. LCI/LCA (Renda Fixa / Baixo Risco / Mínimo R$ 1.000,00 / Isento IR)
4. Fundo Imobiliário - FII (Fundo / Médio Risco / Renda Mensal de Aluguéis)
5. Fundo de Ações (Fundo / Alto Risco / Oscilação de Mercado de Longo Prazo)
```
