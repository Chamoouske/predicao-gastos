# Visão Geral
Um aplicativo ‘desktop’ para gerir finanças pessoais, com foco em predição de gastos usando machine learning e integração com dados reais (ex: extratos bancários em PDF). Combina UI moderna, persistência de dados e análise preditiva.

# Módulos Principais
1. Gestão de Dados Financeiros (CRUD)
   - Cadastro de Transações:
        - Entrada manual de receitas/despesas (valor, data, categoria, descrição).
        - Categorias customizáveis (ex: alimentação, transporte, lazer).
        - Importação via CSV/Excel (ex: arquivos gerados por bancos).
    - Armazenamento:
      - Banco de dados SQLite (leve e local).
      - Uso de Hibernate/JPA para ORM (opcional, mas recomendado).

2. Visualização e Relatórios
    - Gráficos Interativos:
      - Evolução mensal de receitas vs. despesas (JavaFX LineChart).
      - Distribuição de gastos por categoria (PieChart).
      - Comparativo histórico (ex: "Gasto 10% mais com transporte este mês").

    - Relatórios Exportáveis:
      - PDF (usando Apache PDFBox ou JasperReports).
      - Excel (Apache POI).

3. Predição de Gastos (Machine Learning)
    - Treinamento do Modelo:
      - Coleta de dados históricos (ex: últimos 12 meses).
      - Feature engineering: extração de padrões (ex: gastos sazonais em dezembro).
      - Modelo de regressão linear (previsão de gastos futuros por categoria).

    - Integração na UI:
      - Exibição de previsões em gráficos (ex: linha de tendência).
      - Alertas de gastos incomuns (ex: "Sua conta pode ficar negativa em 7 dias").

4. Reconhecimento de PDF (OCR)
   - Leitura de Extratos Bancários:
     - Upload de PDFs (ex: extratos de cartão de crédito).
     - Extração de texto com Tesseract OCR (via JNA).
     - Parsing automático de valores, datas e categorias.


# Requisitos Detalhados
## Funcionais Avançados:
1. Reconhecimento de Padrões em PDF:
   - Parse PDFs com layouts variados (ex: Itaú, Bradesco).
   - Identificar valores negativos (despesas) vs. positivos (receitas).
   - Mapear descrições para categorias (ex: "Posto Shell" → "Transporte/Combustível").

2. Sistema de Alertas:
   - Notificações em tempo real (ex: popup na bandeja do sistema).
   - Configuração de limites por categoria (ex: "Alerta se gastar > R$500 em lazer").

3. Integração com APIs Externas:
   - Cotação de moedas (ex: via API do BCB).
   - Atualização automática de preços de ativos (ex: ações, criptomoedas).

## Não Funcionais:
- **Performance:** Carregar 10k transações em < 3s.
- **Segurança:** Dados sensíveis (como PDFs) criptografados localmente.
- **Usabilidade:** UI intuitiva com atalhos de teclado (ex: ctrl+N para nova transação).

# Tecnologias Recomendadas
| Módulo           | Tecnologias                                                             |
|------------------|-------------------------------------------------------------------------|
| UI Desktop       | JavaFX (com FXML para layouts), ControlsFX (componentes avançados)      |
| Persistência     | SQLite + Hibernate, Flyway (migrações de banco)                         |
| Machine Learning | Tribuo (para ML) ou WEKA (alternativa mais simples)                     |
| PDF/OCR          | Apache PDFBox (leitura de PDF), Tesseract OCR (reconhecimento de texto) |
| Exportação       | Apache POI (Excel), JasperReports (PDF)                                 |
| Concorrência     | JavaFX Concurrent API (Tasks/Service) para não bloquear a UI            |

# Desafios Técnicos & Soluções
1. Parsing de PDFs Complexos:
   - Problema: Layouts variados dificultam a extração de dados.
   - Solução: Usar expressões regulares (regex) para identificar padrões (ex: datas no formato dd/MM/yyyy).

2. Treino do Modelo de ML:
   - Problema: Dados desbalanceados (ex: poucas transações em certas categorias).
   - Solução: Aplicar técnicas de oversampling ou usar modelos robustos a desbalanceamento.

3. Desempenho da UI:
   - Problema: Gráficos com muitos dados travam a interface.
   - Solução: Paginação ou amostragem de dados para visualização.

