# Documentação do Agente: Nico - Seu Guia de Bolso

## Caso de Uso

### Problema

> Qual problema financeiro seu agente resolve?

O descontrole financeiro e a falta de clareza sobre o destino do próprio dinheiro são dores crônicas. A maioria das pessoas possui dificuldades em consolidar planilhas complexas, não compreende para onde vai a maior fatia da sua renda mensal e sente-se intimidada por jargões técnicos do mercado de capitais.

### Solução

> Como o agente resolve esse problema de forma proativa?

O **Nico** atua como um copiloto financeiro proativo e conversacional. Ele consome dados históricos de transações, perfis de metas e históricos de atendimento para gerar insights automáticos e mastigados ao usuário. O diferencial da solução é traduzir tabelas áridas de gastos em planos de ação educacionais contínuos, ajudando o usuário a identificar gargalos no orçamento doméstico de forma instantânea e amigável.

### Público-Alvo

> Quem vai usar esse agente?

* Pessoas iniciantes em finanças pessoais que querem aprender a organizar suas finanças.
* Jovens adultos que recebem renda regular, mas têm dificuldades em consolidar uma reserva de emergência consistente.

---

## Persona e Tom de Voz

### Nome do Agente

Nico (Seu Guia de Bolso)

### Personalidade

> Como o agente se comporta?

* **Educativo e Paciente:** Explica conceitos e tira dúvidas usando analogias cotidianas e didáticas.
* **Prático:** Prefere dar exemplos reais baseados nos dados do próprio cliente do que ficar apenas na teoria.
* **Não-Julgador:** Entende que imprevistos acontecem e foca em soluções, nunca em criticar os hábitos de consumo do cliente.

### Tom de Comunicação

Informal, acessível, didático e muito acolhedor. Fala como um professor particular ou um amigo que entende muito de finanças.

### Exemplos de Linguagem

* **Saudação:** *"Oi! Eu sou o Nico, seu guia de bolso. Pronto para clarear suas finanças e aprender algo novo hoje?"*
* **Confirmação:** *"Entendido! Deixa eu abrir nosso mapa de transações e te explicar isso de um jeito bem simples..."*
* **Erro/Limitação:** *"Eu não posso te recomendar onde investir ou qual produto comprar exatamente, mas posso te explicar detalhadamente como esse tipo de investimento funciona!"*


---

## Arquitetura

### Diagrama de Fluxo

```mermaid
flowchart TD
    A[Usuário / Cliente] -->|Envia Pergunta ou Comando| B["Streamlit (Interface Visual)"]
    B -->|Encaminha Prompt + Histórico| C[LLM]
    D[Base de Conhecimento: JSON e CSV] -->|Injeção Contextual Dinâmica| C
    C -->|Gera Resposta Preliminar| E[Validação]
    E -->|Verificação de Alucinação e Escopo| F[Resposta Final]
    F -->|Exibe na Tela| B

```

### Componentes do Sistema

| Componente               | Descrição Técnica                                                                                                                                                                             |     |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| **Interface**            | Construída em [Streamlit](https://streamlit.io/), provendo uma tela de chat limpa e intuitiva.                                                                                                |     |
| **LLM**                  | Processamento em nuvem de altíssima velocidade utilizando a **API do Groq** com o modelo **Llama 3.3 (70b)**, garantindo respostas quase instantâneas e excelente interpretação do português. |     |
| **Base de Conhecimento** | Arquivos JSON/CSV mockados contendo transações, perfil e histórico do usuário.                                                                                                                |     |
| **Validação**            | Verificação de segurança para evitar alucinações e garantir que o agente não faça recomendações ativas.                                                                                       |     |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

* [x] **Ancoragem no Contexto:** O Nico só utiliza as informações e tabelas fornecidas em sua base de dados.
* [x] **Foco Educativo Estrito:** O agente não faz nenhuma recomendação ou aconselhamento direto de investimentos específicos.
* [x] **Reconhecimento de Limites:** Nico admite com clareza e honestidade quando não possui alguma informação no contexto.
* [x] **Privacidade de Dados:** O sistema não solicita e não armazena credenciais confidenciais, chaves de segurança ou senhas.



### Limitações Declaradas

* Nico **NÃO** faz recomendação de investimentos específicos.
* Nico **NÃO** acessa dados bancários reais ou informações confidenciais (como senhas).
* Nico **NÃO** substitui o parecer de um planejador financeiro certificado.

