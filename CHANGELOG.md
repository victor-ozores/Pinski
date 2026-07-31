# Changelog

Todas as mudanças relevantes deste projeto serão documentadas aqui.
Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/).

---

## [1.0.0] - 2026-07-31

### Added
- Lançamento inicial do projeto — Desafio Kickstart, Power BI Experience
- Dashboard com 3 páginas: Vendas, Devoluções, Simulação
- `Dim_Calendario` em DAX, marcada como Date Table, com colunas de identificação temporal, período atual e comparação com período anterior
- Star schema com 2 relacionamentos (`Fact_Vendas → Dim_Produto`, `Fact_Vendas → Dim_Calendario`), ambos ativos e single-direction
- 134 medidas DAX organizadas em display folders por domínio (Vendas, Devoluções, Simulador, Config)
- 7 UDFs DAX (Preview): `fxFormatoMoeda`, `fxFormatoRotulo`, `fxEixoMax`, `fxEixoMin`, `fxSvgMontarCard`, `fxSvgMontarDonut`, `fxSvgMontarGauge`
- Cards KPI em SVG gerado por DAX, com seta de variação e subtexto contextual calculado
- Gauge de Taxa de Devolução (página Devoluções) e Taxa Simulada (página Simulação) em SVG
- Simulador de redução de taxa de devolução por produto, com slicer em pontos percentuais e cálculo de Lucro Extra em tempo real
- Descrições preenchidas em todas as 134 medidas do modelo
- Documento de respostas às 21 perguntas de negócio do case, organizadas em 5 áreas: Exploratória, Carteira de Produtos, Perfil de Clientes, Performance por Loja e Análises Extras

### Fixed
- Gráfico "Faturamento por Produto" corrigido de ordenação alfabética (padrão indevido) para ordenação por medida de quantidade vendida
- Medida de teto de eixo Y do gráfico de Taxa de Devolução por Categoria trocada de agregação por Categoria para agregação por Produto — necessário após adicionar drill-down, já que o maior valor individual por produto pode superar o maior valor agregado por categoria

### Added — Tooltips
- `TT_V_top_10_vendidos` — ranking de produtos por quantidade vendida, corrigindo a limitação do gráfico principal (ordenado por faturamento, não por unidades)
- `TT_V_ticket_medio_produto` — ticket médio por produto
- `TT_V_desconto_perfil_lider` — total de descontos e perfil de gênero líder em faturamento
- `TT_V_tamanho_por_loja` — tamanho mais requerido, contextualizado por loja via hover
- Medida auxiliar `Cfg Trigger Hover Tooltip` — viabiliza tooltip de página de relatório em visuais de imagem (SVG), que não suportam esse recurso nativamente

### Added — Medidas Novas
- `Perfil Lider Faturamento` — perfil de gênero líder em faturamento (equivalente à já existente `Perfil Lider Devolucao`, agora disponível para o lado de vendas)
- `Eixo Max Quantidade Vendida Produto`, `Eixo Max Quantidade Vendida Tamanho`, `Eixo Max Taxa Devolucao Produto` — medidas de eixo dinâmico para os novos gráficos e níveis de drill-down

### Added — Filtros e Segmentação
- Coluna `PeriodoL12M` em `Dim_Calendario`, classificando cada data como "Últimos 12 Meses" ou "Restante" — usada como slicer no gráfico de Faturamento por Loja para responder análises de desempenho no período mais recente, sem afetar os demais visuais da página
- Filtro de UF configurado para excluir o valor `"na"` (identificador do canal Online) em segmentações por estado físico

### Documentation
- README.md com arquitetura, decisões de modelagem, catálogo de medidas e limitações conhecidas do projeto
- Prompt estruturado para geração de apresentação executiva (Claude for PowerPoint), com paleta de cores oficial e tabela de referência de todos os números-chave do case