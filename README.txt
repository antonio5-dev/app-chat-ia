============================================================
 PROJETO: Chat de IA (Gemini) - Web App / PWA
============================================================

Um aplicativo web progressivo (PWA) de chat com inteligência artificial com sistema de memória. 
Projetado para rodar diretamente no navegador ou ser instalado no Celular via Navegador Chrome, utilizar a API do Gemini com total flexibilidade dos modelos gratuitos e gerenciar memórias persistentes de forma inteligente no navegador (IndexedDB).

--- 🚀 CARACTERÍSTICAS PRINCIPAIS ---

1. Integração Direta com a API do Gemini:
   - Escolha entre os três modelos gratuitos da linha Gemini (3.5 Flash Lite, 3.6 Flash, e 3.8 Flash).
   - Controle total de Temperatura diretamente por slider na interface.
   - Ajuste dinâmico de Contexto (número de mensagens anteriores enviadas na requisição).
   - Armazenamento seguro da sua API Key diretamente no LocalStorage do navegador.

2. Sistema Avançado de Memória de Longo Prazo e Perfil:
   - Memória Recente gerencia o fluxo imediato da conversa.
   - Quando o histórico atinge o limite, a própria IA compacta e destila fatos importantes para a Memória Permanente e para o Perfil do Usuário.
   - Gerenciamento completo pelo modal de Memórias (visualização, exclusão seletiva e limpeza geral).

3. Personalização da IA:
   - Edite o prompt de sistema (Personalidade) diretamente no app para moldar o comportamento, o tom e a identidade da assistente ou interlocutora.

4. PWA (Progressive Web App):
   - Totalmente funcional para celular.
   - Botão de instalação nativa para instalar o app no celular.
   - Service Worker otimizado com cache inteligente e fallback dinâmico.

5. Backup e Portabilidade:
   - Funções integradas para Exportar e Importar todo o estado e dados salvos.

--- 📂 ESTRUTURA DOS ARQUIVOS DO PROJETO ---

- index.html   : A interface completa do aplicativo (Frontend, Estilos CSS, Lógica do Chat e IndexedDB).
- manifest.json: Arquivo de manifesto PWA que define nome, cores, ícones e comportamento como app nativo.
- sw.js        : Service Worker para gerenciar o cache de ativos estáticos e o funcionamento offline.
-ícones

--- 🛠️ COMO USAR E EXECUTAR O PROJETO ---

Como este é um aplicativo puramente client-side (HTML, CSS e JavaScript puro, sem backend dedicado), você pode executá-lo de duas formas:

Opção A: Pelo link: https://app-viva-ia.vercel.app
1. Abra o link do projeto no navegador do PC ou do Celular (Google Chrome).
2. No PC: cole sua chave API Gemini e comece a conversar.
3. No Celular: clique em instalar, para instalar o App; Abra, cole sua chave API Gemini e comece a conversar.

Uso Direto
1. Baixe ou clone este repositório.
2. Certifique-se de que os três arquivos (`index.html`, `manifest.json`, `sw.js`) e os ícones PNG estejam na mesma pasta.
3. Dê dois cliques em `index.html` para abrir diretamente no seu navegador (Firefox, Chrome, Edge, etc.).

Opção B: Uso Direto
1. Baixe ou clone este repositório.
2. Certifique-se de que os três arquivos (`index.html`, `manifest.json`, `sw.js`) e os ícones PNG estejam na mesma pasta.
3. Dê dois cliques em `index.html` para abrir diretamente no seu navegador (Firefox, Chrome, Edge, etc.).
 
--- 🔑 PRIMEIROS PASSOS APÓS ABRIR O APP ---

1. Obtenha sua chave de API do Gemini no Google AI Studio.
2. No painel de controles do app, cole sua chave no campo "Cole sua API Key do Gemini aqui" e clique em "Salvar Chave".
3. Escolha o modelo desejado, ajuste a temperatura, a personalidade e comece a conversar!
