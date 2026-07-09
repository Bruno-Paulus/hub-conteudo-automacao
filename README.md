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

## Próximas versões
- v1.1: alerta de hiato de publicação
- v1.2: métricas do Instagram
- v2.0: resumo semanal gerado por IA
