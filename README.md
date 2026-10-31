# Crimes-PR — WebGIS demonstrativo

Aplicação web estática para visualização exploratória de registros sintéticos. O frontend está em `index.html` e usa Leaflet para o mapa e Chart.js para gráficos. Não exige backend; precisa de conexão à internet para carregar as bibliotecas e os mapas-base por CDN.

> **Importante:** `data/estatisticas_sesp.json` contém 72 registros sintéticos criados para testar a interface. Não são dados oficiais da SESP-PR e não devem embasar análises, decisões operacionais ou publicações estatísticas. `data/bairros.geojson` é apenas um modelo vazio.

## Publicar no GitHub Pages

1. Abra **Settings → Pages** neste repositório.
2. Em **Build and deployment**, selecione **Deploy from a branch**.
3. Escolha a branch `main` e a pasta `/(root)`; clique em **Save**.
4. Aguarde o workflow de publicação concluir e abra o endereço mostrado na página Pages.

Se a opção Pages não aparecer, verifique se você está nas configurações do repositório correto e se possui permissão de administrador. O conector usado nesta sessão consegue enviar arquivos e commits, mas não expõe uma ação para alterar a configuração de Pages; por isso, essa etapa pode exigir um clique manual.

## Arquivos

- `index.html`: interface responsiva, filtros por município/ano/mês/tipo, mapa interativo com pontos, gráficos, tabela resumo, exportação CSV e carregamento de arquivo JSON/GeoJSON para teste na sessão.
- `data/estatisticas_sesp.json`: exemplo sintético, com campos de data, município, bairro, tipo, hora e coordenadas.
- `data/bairros.geojson`: modelo vazio de FeatureCollection para futura inclusão de polígonos autorizados.
- `README.md`: documentação.

## Estrutura de dados

O JSON usa a estrutura:

```json
{
  "fonte": "Descrição da fonte",
  "demonstracao": true,
  "atualizado_em": "AAAA-MM-DD",
  "populacao_por_municipio": {},
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

Datas no formato `AAAA-MM-DD`; coordenadas em WGS84/EPSG:4326. Os nomes dos campos podem usar os aliases presentes no código (`date`, `city`, `neighborhood`, `type`, `lat`, `lng`).

## Segurança e qualidade

- O GitHub Pages publica o conteúdo de forma acessível pela web. Confirme autorização institucional antes de disponibilizar qualquer dado real.
- Não publique nomes, documentos, endereços residenciais, identificadores pessoais ou informação protegida.
- Documente fonte, período, conceitos, cobertura, regras de deduplicação e limitações.
- O mapa não geocodifica endereços nem infere coordenadas; exibe apenas coordenadas presentes no arquivo.
- O carregamento de arquivos pelo botão é temporário e vale somente para a sessão atual.
