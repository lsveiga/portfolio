# Agente de Copy para Redes Sociais — Empresa de Engenharia Civil

> Pipeline com IA que transforma um briefing em textos de Instagram fiéis à marca e à regulamentação da profissão.
> Produto da operação **Social Labs MKT**.

**Stack:** n8n · API Anthropic (Claude Sonnet) · Supabase · Cloudflare Pages
**Status:** pipeline mínimo (M1) validado em produção em 25/06/2026; marcos seguintes em roadmap

---

## Objetivo

Dar a uma empresa de engenharia civil um fluxo para produzir posts de Instagram com **consistência de
voz** e sem depender de redator disponível a cada publicação.

## Desafio

Dois riscos tornam esse caso mais difícil que um simples "gerar texto com IA":

1. **Alucinação.** Um modelo de linguagem tende a preencher lacunas: inventa prazos, números de obras, nomes de clientes. Para uma empresa técnica, isso é erro de credibilidade.
2. **Regulamentação profissional.** A comunicação de engenharia tem limites éticos e legais (promessas de aprovação garantida, de prazo ou de economia, por exemplo, não podem aparecer).

## Solução

Um pipeline automatizado: **formulário de briefing → decupação → agente de redação → resposta com 2 versões do texto**.

O agente de redação foi desenhado com regras em ordem de prioridade:

- **Anti-alucinação:** só usa o que está no Brand Playbook ou no briefing. Quando falta informação, declara em um campo `incertezas` em vez de inventar.
- **Compliance:** lista de promessas e termos proibidos embutida no prompt.
- **CTAs e hashtags controlados:** só os previstos no brandbook do cliente.
- **Saída estruturada em JSON**, com tratamento defensivo de respostas mal formatadas do modelo.

O **Brand Playbook** (voz, vocabulário, pilares, CTAs) é a fonte única da verdade e serve de base para qualquer novo agente do cliente.

## Roadmap

| Marco | Status |
|---|---|
| M1 — Pipeline mínimo (formulário → decupação → redação) | Validado em produção |
| M2 — Loop de auto-validação no redator | Planejado |
| M3 — Mini-site de aprovação (React + Supabase) | Em andamento: schema do banco, autenticação e workflow que processa briefings pendentes prontos; interface de aprovação pendente |
| M4 — Entrada por Telegram (áudio e texto) | Planejado |
| M5 — Agente que pergunta quando o briefing é incompleto | Planejado |
| M6 — Geração de arte e segunda aprovação | Planejado |

## Aprendizados

- Regras de compliance **dentro do prompt** com ordem de prioridade funcionam melhor que instruções soltas.
- O modelo às vezes devolve JSON dentro de blocos de código; tratar isso no pipeline evita falhas intermitentes.

## Imagens

Pendente: diagrama do fluxo (formulário → decupação → redação → resposta). Não há tela de usuário final nesta etapa.
