# Hub de Conteúdo — Automação de Métricas

Sistema que centraliza a produção de conteúdo (YouTube, Instagram, Substack) 
em um hub no Notion, com automação via n8n para captura automática de 
métricas de performance.

## O problema

56 conteúdos publicados, zero dado de performance capturado. Toda métrica era preenchida manualmente (quando era preenchida)
— sem visibilidade real do que funcionava. Rodando a primeira automação, 
43 desses conteúdos foram processados com sucesso; os outros 3 revelaram um problema real de dado 
(status "Postado" com data de publicação futura), que ficou visível justamente por causa da automação.

## A solução (v1.0)

Workflow n8n que roda diariamente:
1. Busca no Notion todos os conteúdos com status "Postado" e link do YouTube
2. Extrai o ID de cada vídeo (cobrindo 3 formatos de URL diferentes)
3. Consulta a API do YouTube em lote (até 50 vídeos por chamada)
4. Cruza o resultado com a página correta do Notion
5. Atualiza o campo "Views YouTube" automaticamente

## Stack
- Notion API
- YouTube Data API v3
- n8n (orquestração)

## Como rodar

1. Importe o arquivo `youtube-views-notion-v1.json` no n8n (Menu → Import from File)
2. Crie as credenciais necessárias:
   - **Notion**: conecte via OAuth2 e dê acesso à sua database de conteúdos
   - **YouTube Data API v3**: gere uma chave em [console.cloud.google.com](https://console.cloud.google.com), ativando a API "YouTube Data API v3"
3. Ajuste os nomes das propriedades da sua database do Notion nos nodes 
   "Get many database pages" e "Update a database page" para bater com 
   os nomes das suas colunas
4. Ative o workflow (Publish) — ele roda automaticamente todo dia às 6h




## Próximas versões
- v1.1: alerta de hiato de publicação
- v1.2: métricas do Instagram
- v2.0: resumo semanal gerado por IA
