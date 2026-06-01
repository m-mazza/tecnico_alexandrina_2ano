# Semana 12
**Assunto: Conceitos — Otimização de Performance em Aplicações Web e React**
---

## 1. Técnicas de Otimização de Performance

### 1.1 Code Splitting
Divisão do código JavaScript em partes menores (chunks), que são carregadas sob demanda, reduzindo o tamanho do bundle inicial da aplicação.

### 1.2 Lazy Loading
Técnica que adia o carregamento de recursos (imagens ou componentes) até o momento em que eles são realmente necessários — por exemplo, quando o usuário rola a página até aquele elemento.

- **Lazy Loading de Imagens**: feito com o atributo HTML nativo `loading="lazy"` na tag `<img>`.
- **Lazy Loading de Componentes (React)**: feito com `React.lazy()` em conjunto com `<Suspense>`, que exibe um fallback enquanto o componente é carregado.

### 1.3 Memoization (`React.memo()`)
Técnica que memoriza o resultado de renderização de um componente funcional. O componente só é re-renderizado quando suas props mudam, evitando renderizações desnecessárias.

### 1.4 Minificação
Processo de reduzir o tamanho dos arquivos JavaScript, CSS e HTML removendo espaços em branco, comentários e outros caracteres desnecessários.

- **JavaScript**: realizada com a biblioteca **Terser** (via `TerserPlugin` no Webpack).
- **CSS**: realizada com a biblioteca **CSSNano** (via `CssMinimizerPlugin` no Webpack).
- **Create React App**: a minificação de JS, CSS e HTML é feita automaticamente ao executar `npm run build`.

### 1.5 Pure Components (`React.PureComponent`)
Componentes de classe que realizam uma comparação rasa (shallow comparison) das props e do estado antes de re-renderizar. Se não houver mudanças, a renderização é ignorada, evitando trabalho desnecessário.

### 1.6 Virtualização de Listas (`react-window`)
Técnica que renderiza apenas os itens da lista visíveis na tela, em vez de renderizar todos os itens ao mesmo tempo. À medida que o usuário rola a tela, novos itens são carregados. Utilizada com a biblioteca **react-window** (`FixedSizeList`).

---

## 2. Métricas de Performance

### 2.1 First Contentful Paint (FCP)
Tempo até que o primeiro conteúdo da página (texto, imagem, etc.) seja renderizado no navegador.

### 2.2 Largest Contentful Paint (LCP)
Tempo até que o maior elemento visível da página seja carregado e renderizado.

### 2.3 Time to Interactive (TTI)
Tempo até que a página esteja completamente interativa — ou seja, pronta para responder às ações do usuário.

### 2.4 Total Blocking Time (TBT)
Tempo total durante o qual a thread principal do navegador ficou bloqueada por scripts pesados, impedindo a interação do usuário.

### 2.5 Cumulative Layout Shift (CLS)
Métrica de estabilidade visual. Mede o quanto os elementos da página se movem de forma inesperada durante o carregamento.

### 2.6 First Byte Time (TTFB — Time to First Byte)
Tempo decorrido desde a requisição até o recebimento do primeiro byte de resposta do servidor.

### 2.7 Start Render
Momento em que algo visível começa a ser exibido na página pela primeira vez.

### 2.8 Speed Index
Velocidade geral percebida de carregamento da página, considerando o quão rápido o conteúdo visível aparece.

### 2.9 Fully Loaded
Momento em que todos os recursos da página (imagens, scripts, fontes, etc.) foram completamente carregados.

---

## 3. Ferramentas de Análise de Performance

### 3.1 Google Lighthouse
Ferramenta integrada ao Chrome DevTools (aba **Lighthouse**) que gera relatórios com pontuações para **Performance**, **Acessibilidade**, **Boas Práticas** e **SEO**. Permite análise em dispositivos Desktop ou Mobile.

### 3.2 WebPageTest
Serviço online (webpagetest.org) para diagnóstico detalhado do tempo de carregamento em diferentes condições de rede (4G, 3G, Desktop) e localizações geográficas. Gera um **Waterfall Chart** (gráfico em cascata) que mostra o tempo de carregamento de cada recurso individualmente.

### 3.3 Chrome DevTools — Aba Network
Permite monitorar em tempo real todos os recursos carregados pela página (scripts, CSS, imagens), exibindo tamanho dos arquivos, tempo de resposta e número de requisições. Permite filtrar por tipo de recurso.

### 3.4 Chrome DevTools — Aba Performance
Permite gravar a execução da página e visualizar as fases de carregamento: **Loading**, **Scripting**, **Rendering** e **Painting**. Exibe eventos como **First Paint** e **DOMContentLoaded**.

---

## 4. Conceitos de Ferramentas e Ecossistema

### 4.1 Webpack
Empacotador (bundler) de módulos JavaScript. Permite configurar plugins de otimização como `TerserPlugin` (minificação de JS) e `CssMinimizerPlugin` (minificação de CSS).

### 4.2 Create React App
Ferramenta oficial para criar projetos React com configuração zero. Inclui automaticamente minificação, Code Splitting e outras otimizações ao executar `npm run build`.

### 4.3 React.lazy()
Função do React que permite importar componentes de forma dinâmica (carregamento sob demanda), habilitando o Code Splitting em nível de componente.

### 4.4 Suspense
Componente do React usado em conjunto com `React.lazy()`. Exibe um conteúdo de fallback (ex.: "Carregando...") enquanto o componente dinâmico está sendo carregado.

### 4.5 react-window
Biblioteca JavaScript para virtualização de listas e grades em React. O componente principal usado é o `FixedSizeList`, que renderiza apenas os itens visíveis na janela de visualização.

### 4.6 react-router-dom
Biblioteca de roteamento para React. Permite criar rotas e navegar entre páginas/componentes dentro de uma aplicação.

### 4.7 Waterfall Chart (Gráfico em Cascata)
Representação visual gerada por ferramentas como WebPageTest e Chrome DevTools que mostra, em ordem cronológica, o carregamento de cada recurso de uma página, facilitando a identificação de gargalos.

### 4.8 DevTools (Chrome Developer Tools)
Conjunto de ferramentas de desenvolvimento integrado ao Google Chrome, acessado pela tecla **F12**. Contém abas como Network, Performance, Lighthouse, entre outras.
