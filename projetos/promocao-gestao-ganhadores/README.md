# Promoção de Supermercado — Landing Page e Gestão de Ganhadores

> Hotsite de campanha promocional de supermercado com painel para cadastro e consulta pública de ganhadores.
> Projeto desenvolvido para a **Solo Propaganda**, cliente final: rede regional de supermercados.

**Stack:** HTML · Tailwind CSS · JavaScript · PHP · MySQL · Swiper
**Status:** entregue; campanha de 2026, com cerca de seis semanas de duração

---

## Objetivo

Comunicar a promoção (R$ 100 mil em prêmios, com sorteios diários) e dar **transparência** ao resultado, com uma página pública onde qualquer participante pesquisa se ganhou.

## Desafio

- **Prazo curto:** a campanha tinha data de lançamento fixa e a arte já vinha pronta do design.
- **Hospedagem limitada:** o cliente só dispunha de FTP, sem Node, sem build e sem serviços externos.
- **Operação por não técnicos:** quem registra os ganhadores é a equipe do supermercado, que precisa de um painel simples e seguro.
- **Fidelidade visual:** a identidade vinha de arquivos de design (PSD) com tipografia própria.

## Solução

**Site público**
- Landing page responsiva com versões desktop e mobile de cada seção, menu flutuante, carrossel de parceiros e links para regulamentos.
- Página de **ganhadores com busca por nome**, alimentada por uma API em PHP.

**Painel administrativo (PHP próprio)**
- Login com perfis de acesso (roles).
- Cadastro de ganhadores, **importação em lote por CSV** com planilha-modelo e **upload de foto**.
- Gestão de usuários e perfil.
- Tutorial passo a passo, em imagens, para o operador.

## Decisões técnicas

- **Stack mínima, sem build:** HTML + Tailwind via CDN + JS puro. Edita, salva, sobe por FTP. Em uma campanha de poucas semanas, isso elimina o risco de quebrar o deploy no dia do lançamento.
- **Mudança de rota durante o projeto:** o plano inicial previa Supabase; ao confirmar o ambiente de hospedagem, o projeto evoluiu para **PHP + MySQL** no próprio provedor do cliente. O plano original foi mantido como registro, com um documento de estado apontando qual é a fonte da verdade.
- **Documento de estado do projeto** para que qualquer pessoa assuma a manutenção sem refazer o raciocínio.

## Observação

Código-fonte, base de dados e dados de ganhadores pertencem ao cliente e **não são publicados**.

## Imagens

Pendente: capturas da landing e da página pública, após definir o que pode ser exibido sem identificar o cliente.
