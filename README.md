# Crimes-PR — WebGIS demonstrativo

Aplicação web estática para visualização exploratória de registros **sintéticos**. Não exige backend; Leaflet, Chart.js e mapas-base são carregados por CDN e requerem conexão à internet.

> **Importante:** `data/estatisticas_sesp.json` contém registros sintéticos para testar a interface. Não são dados oficiais da SESP-PR e não devem embasar análises, decisões operacionais ou publicações estatísticas. `data/bairros.geojson` é apenas um modelo vazio.

## Publicação automática com GitHub Actions

O workflow `.github/workflows/pages.yml` valida os arquivos e publica o site no GitHub Pages a cada push para `main`, além de permitir execução manual.

### Configuração inicial (uma única vez)

1. Abra **Settings → Pages** neste repositório.
2. Em **Build and deployment → Source**, selecione **GitHub Actions** (não “Deploy from a branch”).
3. Abra a aba **Actions** e acompanhe **Deploy Crimes-PR to GitHub Pages**.
4. Quando a execução terminar com sucesso, abra o endereço publicado no ambiente `github-pages` ou em **Settings → Pages**.

Endereço esperado: https://laistheodoro.github.io/Crimes-PR/.

### Diagnóstico

- **Build falhou:** abra a execução em Actions e consulte a etapa vermelha.
- **Deploy falhou por permissões:** confirme que Pages está configurado como **GitHub Actions** e que o workflow tem `pages: write` e `id-token: write`.
- **404 logo após publicar:** aguarde alguns minutos e use o endereço exibido em Settings → Pages; confirme que o job Deploy terminou com sucesso.
- O workflow verifica a presença de `index.html` e do JSON de demonstração e valida a sintaxe do JSON.

## Arquivos

- `index.html`: interface responsiva, filtros por município/ano/mês/tipo, mapa, gráficos, tabela-resumo, exportação CSV e carregamento temporário de JSON/GeoJSON.
- `data/estatisticas_sesp.json`: dados de exemplo sintéticos.
- `data/bairros.geojson`: modelo vazio de FeatureCollection.
- `.github/workflows/pages.yml`: validação e publicação automática.
- `README.md`: documentação.

## Estrutura de dados

O JSON pode conter metadados e uma lista `ocorrencias`:

```json
{
  "fonte": "Descrição da fonte",
  "demonstracao": true,
  "atualizado_em": "AAAA-MM-DD",
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

Datas em `AAAA-MM-DD`; coordenadas em WGS84/EPSG:4326. O frontend também reconhece aliases como `date`, `city`, `neighborhood`, `type`, `lat` e `lng`.

## Segurança e qualidade

- O GitHub Pages publica conteúdo acessível pela web. Confirme autorização institucional antes de disponibilizar dados reais.
- Não publique nomes, documentos, endereços residenciais, identificadores pessoais ou informação protegida.
- Documente fonte, período, conceitos, cobertura, regras de deduplicação e limitações.
- O mapa exibe apenas coordenadas presentes nos arquivos; não geocodifica endereços.
- Arquivos carregados pela interface ficam apenas na sessão atual e não são enviados ao repositório.
