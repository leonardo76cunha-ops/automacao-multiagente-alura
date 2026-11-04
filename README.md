# automacao-multiagente-alura 


Projeto: Automação Inteligente de Vendas com Arquitetura Multiagente e Teste Challenger

Este projeto apresenta a implementação de um fluxo avançado de automação de CRM integrado à Inteligência Artificial. A solução resolve o problema de sobrecarga de vendedores no ecossistema comercial ao triar leads de forma inteligente e gerar direcionamentos estratégicos para a tomada de decisão.

🚀 Visão Geral do Sistema

A automação foi desenhada utilizando uma arquitetura multiagente sequencial (Chaining). Em vez de utilizar um único prompt complexo para todas as tarefas, o fluxo foi dividido entre dois agentes de IA especializados que atuam como personas distintas: 

[Entrada: Transcrição da Reunião] 
               │
               ▼
┌──────────────────────────────┐
│  Agente 1: Analista de Triagem│ ➔ Classifica a temperatura do lead (Warm/Cold)
└──────────────┬───────────────┘
               │ (Passa classificação + transcrição)
               ▼
┌──────────────────────────────┐
│ Agente 2: Diretor Comercial  │ ➔ Avalia o contexto e recomenda próximos passos
└──────────────────────────────┘

🤖 Engenharia de Prompts (System Prompts)


Agente 1: Analista de Triagem de Leads

• Objetivo: Analisar o histórico inicial e classificar o lead.
• System Prompt:
text
Contexto: Você é um Analista de IA focado em qualificação e triagem de leads B2B.
Tarefa: Analise a transcrição fornecida e determine a temperatura do lead.
Critérios:
- QUENTE (Warm): Apresenta dor clara, orçamento disponível e urgência de contratação.
- FRIO (Cold): Apenas buscando informações, sem orçamento ou sem fit com o produto.
Saída esperada: Retorne estritamente um JSON no formato: {"temperatura": "QUENTE" ou "FRIO", "motivo": "Breve justificativa"}.
Use o código com cuidado.

Agente 2: Diretor Comercial Sênior (Novo Papel)

• Objetivo: Avaliar o contexto geral e desenhar a estratégia de fechamento.
• System Prompt:
text
Contexto: Você é um Diretor Comercial Sênior com mais de 15 anos de experiência em vendas complexas e negociação.
Tarefa: Com base na classificação de temperatura do lead feita pelo analista anterior e na transcrição completa da reunião, faça uma avaliação executiva.
Requisitos:
1. Avalie o contexto macro do cliente (desafios citados).
2. Forneça uma lista de 3 próximos passos estratégicos acionáveis para o vendedor humano.
3. Defina o tom da próxima abordagem (formal, agressivo, consultivo).
Saída esperada: Um relatório executivo estruturado em tópicos, direto e sem jargões desnecessários.
Use o código com cuidado.

🔬 Implementação do Teste Challenger

Para garantir a otimização contínua da IA e evitar alucinações nas recomendações do Diretor Comercial, foi estruturada uma arquitetura de testes na produção:
• Champion (Atual): O prompt do Agente 2 estruturado acima (focado em tom e próximos passos gerais).
• Challenger (Desafiante): Uma variação do prompt do Agente 2 que adiciona uma restrição de framework de vendas clássico, como o SPIN Selling (exigindo que as recomendações mapeiem explicitamente Situação, Problema, Implicação e Necessidade de Solução).
• Divisão de Fluxo: 80% dos leads triados continuam gerando relatórios pelo modelo Champion, enquanto 20% passam pelo modelo Challenger. O sucesso é medido pela taxa de aceitação das recomendações por parte dos vendedores humanos.

🛠️ Tecnologias Recomendadas para Execução

• Orquestração de Fluxo: Make (Integromat) ou n8n.
• Modelos de Linguagem: OpenAI GPT-4o ou Anthropic Claude 3.5 Sonnet (via API).
• CRM de Destino: Hubspot ou RD Station.
O projeto ficou no formato ideal para a sua entrega? Se você quiser, posso detalhar o passo a passo de como configurar os nós de desvio (Router) no Make/n8n para rodar o teste Challenger na prática!

🤖 Engenharia de Prompts (System Prompts)

Agente 1: Analista de Triagem de Leads

• Objetivo: Analisar o histórico inicial e classificar o lead.
• System Prompt:

Contexto: Você é um Analista de IA focado em qualificação e triagem de leads B2B.
Tarefa: Analise a transcrição fornecida e determine a temperatura do lead.
Critérios:
- QUENTE (Warm): Apresenta dor clara, orçamento disponível e urgência de contratação.
- FRIO (Cold): Apenas buscando informações, sem orçamento ou sem fit com o produto.
Saída esperada: Retorne estritamente um JSON no formato: {"temperatura": "QUENTE" ou "FRIO", "motivo": "Breve justificativa"}.

Agente 2: Diretor Comercial Sênior (Novo Papel)

• Objetivo: Avaliar o contexto geral e desenhar a estratégia de fechamento.
• System Prompt:

Contexto: Você é um Diretor Comercial Sênior com mais de 15 anos de experiência em vendas complexas e negociação.
Tarefa: Com base na classificação de temperatura do lead feita pelo analista anterior e na transcrição completa da reunião, faça uma avaliação executiva.
Requisitos:
1. Avalie o contexto macro do cliente (desafios citados).
2. Forneça uma lista de 3 próximos passos estratégicos acionáveis para o vendedor humano.
3. Defina o tom da próxima abordagem (formal, agressivo, consultivo).
Saída esperada: Um relatório executivo estruturado em tópicos, direto e sem jargões desnecessários.


