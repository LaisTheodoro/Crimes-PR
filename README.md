# Crimes-PR — WebGIS

Aplicação estática para GitHub Pages. O frontend fica em `index.html` (HTML, CSS e JavaScript em um único arquivo), sem Node.js ou backend.

> **Dados de demonstração:** `data/estatisticas_sesp.json` contém registros sintéticos. Não são estatísticas oficiais da SESP-PR. `data/bairros.geojson` é um modelo vazio; substitua-o por polígonos válidos autorizados para habilitar o coroplético.

## Publicação pelo GitHub Pages
1. Envie `index.html`, a pasta `data/` e este README para a raiz da branch `main`.
2. No GitHub, abra **Settings → Pages**.
3. Em **Build and deployment**, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`, e salve.
4. Aguarde a publicação e abra o endereço fornecido pelo GitHub Pages.

A aplicação carrega bibliotecas e mapas externos via CDN; é necessária conexão com a internet. Para testar localmente, use um servidor HTTP, não abra o HTML via `file://`.

## Dados tabulares
Atualize `data/estatisticas_sesp.json` preservando uma estrutura como:

```json
{
  "fonte": "SESP-PR — base/relatório e referência",
  "demonstracao": false,
  "atualizado_em": "2026-10-31",
  "populacao_por_municipio": {"Curitiba": 1773718},
  "ocorrencias": [{
    "id": "identificador não pessoal",
    "data": "2026-01-15",
    "municipio": "Curitiba",
    "bairro": "Centro",
    "tipo": "Furto",
    "hora": 14,
    "latitude": -25.432,
    "longitude": -49.271
  }]
}
```

Campos reconhecidos incluem `data`/`date`, `municipio`/`city`, `bairro`/`neighborhood`, `tipo`/`type`, `hora`/`hour`, `latitude`/`lat` e `longitude`/`lng`. Data recomendada: `AAAA-MM-DD`; hora: inteiro entre 0 e 23; coordenadas: WGS84/EPSG:4326.

A taxa por 100 mil habitantes só aparece quando houver população de referência para o município selecionado. Documente o ano e a fonte da população. A variação anual compara os dois anos selecionados com os demais filtros aplicados.

## Limites geográficos
Substitua `data/bairros.geojson` por um `FeatureCollection` GeoJSON em WGS84 (EPSG:4326). Inclua o nome do bairro em `bairro`, `nome_bairro`, `nome`, `name` ou `NM_BAIRRO`. A vinculação com a tabela é feita pelo nome, portanto padronize grafia e acentuação. Dados agregados por bairro não devem ser convertidos em pontos artificiais.

## Funcionalidades
- Filtros por município, ano, ano de comparação, mês, tipo e turno.
- Mapa de pontos, mapa de calor e coroplético (quando há polígonos).
- Camadas base clara, OpenStreetMap, escura e satélite.
- Indicadores, ranking, gráficos, comparação de bairros.
- Exportação CSV e tentativa de exportação PNG.
- Carregamento de JSON/GeoJSON local para a sessão de teste.

## Cuidados
- O GitHub Pages publica os arquivos de forma pública; confirme autorização institucional antes de publicar dados da SESP-PR.
- Não publique nomes, documentos, endereços residenciais, identificadores pessoais ou informações protegidas.
- Valide duplicidades, coordenadas, datas, nomenclaturas, conceitos e limitações metodológicas.
- A exportação PNG pode falhar se o provedor de mapas bloquear captura por CORS.
