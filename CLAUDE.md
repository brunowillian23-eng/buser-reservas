# Ferramenta Interna Buser — Reservas

## O que é
Painel web single-page (`index.html`) hospedado no GitHub Pages:
**https://brunowillian23-eng.github.io/buser-reservas/**

Uso interno da equipe de operações da Buser. Permite importar planilhas de passageiros, agrupar reservas por família/grupo, gerar texto para Jira e juntar PDFs de passagens.

## Tecnologia
- HTML + CSS + JS puro, sem framework
- Fonte: Poppins (Google Fonts)
- Design: Buser Andromeda Design System (`#f11075` como cor primária)
- Bibliotecas via CDN: xlsx 0.18.5, html2canvas 1.4.1, jsPDF 2.5.1, jspdf-autotable 3.8.2, ExcelJS 4.3.0, pdf-lib 1.17.1

## Funcionalidades
1. **Agrupar Reservas** — importa XLS/XLSX/CSV, detecta colunas automaticamente, agrupa passageiros por código de reserva e e-mail, exporta em PNG, PDF e Excel colorido
2. **Juntar Passagens** — merge de PDFs/imagens de passagens em um único PDF
3. **Gerar Texto Jira** — formulário com autocomplete de cidades, empresas e rodoviárias para gerar texto padronizado de chamados

## Arquitetura
- Arquivo único: `index.html` (todo CSS, JS e HTML inline)
- `dadosTabela[]` — array central com os dados importados
- `getDadosParaExportar()` — retorna dados filtrados ou completos para exports
- `DB_CIDADES`, `DB_EMPRESAS`, `DB_RODOVIARIAS` — objetos JS com dados estáticos
- Filtros de embarque/desembarque afetam a tabela E todos os exports (PNG, PDF, Excel)

## Decisões técnicas importantes
- jsPDF não renderiza caracteres não-ASCII → usar `pdfStr()` para converter acentos
- ExcelJS usado para Excel colorido (grupos com cores)
- Agrupamento: reservas com mesmo código OU mesmo e-mail são fundidas no mesmo grupo
- O endereço da rodoviária é preenchido automaticamente pela cidade de **embarque** (não destino)
- Dark mode via `[data-theme]` + `prefers-color-scheme`, preferência salva em localStorage

## Como subir alterações
```bash
git add index.html
git commit -m "descrição da mudança"
git push
```
GitHub Pages atualiza em ~1 minuto.

## Repositório
- GitHub: `brunowillian23-eng/buser-reservas`
- Branch: `main`
- GitHub Pages: ativado na raiz do branch main
