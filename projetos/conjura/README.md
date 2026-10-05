# Conjura — Hub de Criação de Peças de CRM com IA

> Plataforma multi-tenant para criar, aprovar e exportar peças de CRM (e-mail, WhatsApp, push e SMS) com apoio de IA.
> Produto da operação **Social Labs MKT**. *"Conjura" é nome de trabalho; o produto foi desenhado para que trocar o nome seja uma alteração de uma linha.*

**Stack:** Next.js · TypeScript · Supabase (PostgreSQL + RLS) · Claude (Anthropic API) · MJML
**Status:** 🏗️ em construção. Fundação do banco concluída e testada; fluxo de campanhas e aprovação já funcionando na aplicação; geração por IA ainda por vir

---

## Objetivo

Comprimir o ciclo de produção de peças de comunicação de um time de CRM em um **fluxo único com rastro de versão**: briefing → geração multicanal → preview fiel → aprovação → exportação.

## Desafio

O gargalo de um time de CRM não é a ferramenta de disparo, é **produzir a peça**: briefing por e-mail, designer, redator, idas e voltas de aprovação em PDF e WhatsApp, e um HTML montado à mão que quebra no Outlook.

Restrições que moldaram o projeto:

- **Usuários sem familiaridade técnica.** Se uma tela precisa de treinamento, a tela está errada.
- **Governança de empresa grande.** Quem cria não aprova, nem a própria peça, e isso precisa valer no banco, não só na interface.
- **Isolamento entre clientes.** Dados de uma organização jamais podem aparecer para outra.
- **IA com limites.** A IA não gera o produto nem texto dentro da imagem, para evitar erro em material regulado.

## Solução (desenho)

Fluxo principal:

1. Campanha → 2. Canais → 3. Origem (do zero, de template ou reaproveitando peça aprovada) → 4. Briefing estruturado + campo livre → 5. Preview fiel por canal (bolha de WhatsApp, e-mail renderizado, push, SMS com contagem) → 6. Fila do aprovador → 7. Nova versão com as observações já no contexto da IA → 8. Exportação granular ou em pacote.

**Fronteiras conscientes:** o sistema não dispara campanha, não gerencia base de contatos e não mede performance de envio. Essa decisão mantém o produto pequeno o bastante para ser excelente.

## O que já está construído

- **10+ migrations** versionadas, com checksum: migration aplicada não pode ser editada, só substituída por outra. Evita divergência silenciosa entre desenvolvimento e produção.
- **Row Level Security** em todas as tabelas, com isolamento por organização.
- **Máquina de estados** da peça, regra de aprovação e trilha de auditoria.
- **Suíte com cerca de 110 asserções** rodando contra um Postgres local; o comando de publicação **aborta se qualquer teste falhar**.
- **Views de dashboard** que medem a *produção* (volume, tempo de aprovação, taxa de devolução).

## Disciplina de verificação

Uma auditoria ao fim da Fase 0 encontrou, consultando o catálogo do banco e **tentando explorar**, uma função `SECURITY DEFINER` aberta indevidamente que permitiria forjar um evento na organização de outro cliente. Nenhum teste existente pegava. A correção veio junto com um **teste de invariante**, para que a classe inteira de erro não volte. Esse método, auditar atacando em vez de reler o próprio código, virou prática do projeto.

## Documentação

O projeto tem documentação de produto e arquitetura em camadas: visão, arquitetura (modelo de dados, motor de arte, motor de e-mail, camada de IA, segurança), roadmap por fases ordenadas por **risco derrubado**, análise de referência e marca de demonstração.

## Camada de aplicação (já funcionando)

- **Autenticação:** entrada com Google como caminho principal e por código de 8 dígitos como alternativa, com cadastro fechado (só entra quem foi convidado) e encerramento de sessão por inatividade.
- **Equipe:** convite de pessoas, com o portão de autorização **no banco**, não só na tela.
- **Campanhas e peças:** lista, criação, editor de conteúdo por campo com contador de caracteres.
- **Aprovação:** envio para a fila do aprovador, decisão (aprovar ou solicitar alteração) e **"Iniciar V2"** a partir da alteração pedida.
- **Teste A/B** modelado como duas peças irmãs, cada uma com governança de aprovação independente.

## Próximos passos

Motor de arte e geração por IA, conforme o roadmap. Sem prazo fixo: a ordem é o roadmap, não o calendário.

## Observação

Projeto em desenvolvimento; código em repositório privado.

## Imagens

Adicionar em [`imagens/`](imagens/): diagrama do fluxo, esquema de estados da peça, peças da marca de demonstração.
