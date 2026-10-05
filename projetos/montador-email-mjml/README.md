# Montador de E-mail Marketing (MJML)

> Editor visual para montar e-mails marketing responsivos sem escrever HTML.
> Ferramenta interna desenvolvida para a **Solo Propaganda**, parte do hub de ferramentas da agência.

**Stack:** HTML/CSS/JS · MJML · PHP (upload de imagens)
**Status:** em produção

---

## Objetivo

Reduzir o tempo e a dependência técnica na produção de e-mail marketing: montar a peça, ver o
resultado e exportar um HTML pronto para a plataforma de disparo.

## Desafio

E-mail é um dos ambientes mais hostis do front-end: cada cliente de e-mail (Outlook, Gmail, Apple Mail)
interpreta o HTML de um jeito. Montar à mão exige tabelas aninhadas e tratamento de compatibilidade,
e qualquer ajuste pequeno vira retrabalho de quem sabe programar.

Outro ponto de atrito: as imagens do e-mail precisam estar hospedadas em um endereço público antes do
envio, o que gera um passo manual extra para quem monta a peça.

## Solução

- **Montador visual** que gera a estrutura em **MJML**, linguagem que compila para HTML de e-mail compatível com os principais clientes, eliminando o trabalho manual com tabelas.
- Funciona **no navegador do usuário**, sem instalação, alinhado ao requisito de que a equipe não precise configurar nada.
- **Endpoint PHP de upload** (`backend/upload.php`) para publicar as imagens da peça em endereço público, fechando o fluxo "montar → hospedar imagens → exportar".

## Decisões técnicas

- Gerar MJML e não HTML cru: a compatibilidade entre clientes de e-mail fica a cargo do compilador.
- Front sem build (sem npm), para qualquer pessoa da operação abrir e usar.
- Configuração sensível do upload fora do repositório (arquivo local de exemplo versionado, valores reais não).

## Imagens

Adicionar em [`imagens/`](imagens/): tela do montador e um e-mail resultante.
