# Chat de IA (Gemini) — Web App / PWA

🇧🇷 Português · 🇺🇸 [English](README.md)

Um aplicativo web progressivo (PWA) para conversar com inteligência artificial. Roda inteiramente no navegador, fala direto com a API do Google Gemini e guarda a memória de longo prazo no seu próprio aparelho (IndexedDB). Tem várias conversas, entrada por voz, respostas faladas, imagens e documentos.

---

## 🚀 Características

**Chat**
- Várias conversas: crie, renomeie e apague pelo menu ☰.
- Três modelos Gemini à escolha (3.5 Flash Lite, 3.6 Flash, 3.8 Flash).
- Controle de temperatura e de contexto (quantas mensagens anteriores da conversa aberta são enviadas).
- Prompt de sistema editável ("Personalidade"), com botão "Restaurar padrão".
- Idioma das respostas da IA: igual ao da sua mensagem (padrão), inglês ou português.

**Memória de longo prazo (compartilhada entre todas as conversas)**
- As mensagens de todas as conversas alimentam uma única fila de memória.
- Quando 20 mensagens estão esperando, a IA resume as 15 mais antigas em até 5 memórias *Permanentes* e até 5 fatos de *Perfil* sobre você.
- Quando Permanentes ou Perfil chegam a 20 itens, são condensados de novo em 5.
- Todas as conversas enxergam o mesmo Perfil e as mesmas memórias Permanentes. O histórico de mensagens continua separado por conversa.
- Um contador mostra quantas mensagens estão esperando para serem resumidas (por exemplo `7/20`).
- O menu ☰ tem um quadro retrátil **Ainda não resumidas**, que lista essas mensagens de todas as conversas. Apague as que você não quer que sejam lembradas, para que lixo nunca chegue às memórias Permanentes ou de Perfil. Apagar ali só tira a mensagem da memória; ela continua na conversa.
- **Memórias** (em ⚙) lista as memórias Permanentes e de Perfil e mostra o mesmo contador.
- Nas três listas (ainda não resumidas, Permanentes, Perfil) dá para apagar itens um a um, selecionar vários ou apagar todos.
- Apagar uma conversa não apaga as memórias já extraídas dela.

**Voz**
- 🎤 Reconhecimento de fala: toque, fale, e o texto é enviado quando você para (dá para desligar o envio automático).
- 🔊 Respostas faladas: leitura automática ou por mensagem, com **controle de velocidade (0,5×–2×)** e escolha de voz.
- Modo mãos-livres: ouve → responde → fala → volta a ouvir.
- O idioma da voz é configurado separadamente do idioma da interface (12 opções).

**Imagens e arquivos**
- 📎 Anexe imagens (câmera ou galeria no celular; colar ou arrastar no PC). As imagens são comprimidas no aparelho antes do envio.
- PDF: enviado direto ao Gemini (até ~14 MB).
- Word (`.docx`) e OpenDocument (`.odt`): o texto é extraído no navegador.
- Arquivos de texto: `.txt`, `.md`, `.csv`, `.json`, `.html`, código-fonte e similares (primeiros 300.000 caracteres).
- O conteúdo completo dos anexos só é enviado nas 2 últimas mensagens que têm anexo; as anteriores aparecem para a IA apenas como nome de arquivo.

**Interface e PWA**
- Interface em inglês (padrão) e português (BR).
- Botão de instalação para celular ou PC. Um service worker guarda o app em cache (para conversar ainda é preciso internet).
- Exportar / Importar todas as conversas e memórias (backups de versões antigas também podem ser importados).

---

## 📂 Arquivos do projeto

| Arquivo | Função |
|---|---|
| `index.html` | O app inteiro: interface, estilos, lógica do chat, IndexedDB |
| `manifest.json` | Manifesto PWA: nome, cores, ícones |
| `sw.js` | Service worker: cache e funcionamento offline |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | Ícones do app (necessários para a opção de instalar aparecer) |

---

## 🧰 Bibliotecas e requisitos

**O app não tem dependências:** nada de pacotes npm, etapa de build, backend ou CDN. É HTML, CSS e JavaScript puros, usando recursos que já vêm no navegador.

O que você precisa ter:

- **Um navegador moderno baseado em Chromium** (recomendado: Google Chrome; o Microsoft Edge também funciona).
  - O reconhecimento de fala usa a Web Speech API do navegador. Ela existe no Chrome e no Edge, mas não no Firefox. No iPhone/iOS é instável.
  - Ler `.docx`/`.odt` exige um navegador dos últimos anos (Chrome 103 ou mais novo).
- **HTTPS ou `localhost`.** Os navegadores só liberam microfone, service worker e instalação em origem segura. Abrir o `index.html` com duplo clique (`file://`) ou por um endereço da rede local como `http://192.168.x.x` **não** oferece esses recursos.
- **Conexão com a internet.** O chat usa a API do Gemini, e o reconhecimento de fala do Chrome é processado nos servidores do Google.
- **Uma chave de API do Gemini**, criada no [Google AI Studio](https://aistudio.google.com/apikey).
- **Só para a Opção 2 abaixo:** um jeito de servir os arquivos localmente. Python 3 (normalmente já instalado) ou Node.js servem. Qualquer servidor de arquivos estáticos funciona.

---

## 🔒 Privacidade

- Conversas, memórias e anexos ficam só no seu navegador (IndexedDB). A chave de API fica no localStorage do navegador.
- Mensagens, anexos e memórias são enviados à API do Gemini (Google) para gerar as respostas. A voz é enviada pelo Chrome ao serviço de fala do Google.
- Quem tiver acesso ao perfil do seu navegador pode ler a chave de API salva. Use **Exportar** para backups e mantenha os arquivos em local privado, pois eles contêm suas conversas e anexos.

---

## 🛠️ Como usar

### 🔑 Primeiros passos (as duas opções)

1. Crie uma chave de API no [Google AI Studio](https://aistudio.google.com/apikey).
2. Abra o app, toque em ⚙, cole a chave em **Cole sua API Key do Gemini aqui** e toque em **Salvar chave**.
3. Escolha o modelo, a temperatura, a voz e a personalidade, e comece a conversar.

> Se a interface estiver em inglês, troque o idioma em ⚙ → *Interface language* → Português.

### Opção 1 — Usar o site na Vercel (mais fácil)

1. Abra **https://app-viva-ia.vercel.app** no Google Chrome, no PC ou no celular.
2. Celular: toque em **Instalar app** (ou menu ⋮ do Chrome → *Instalar app* / *Adicionar à tela inicial*). PC: clique no ícone de instalar na barra de endereço.
3. Abra o app, coloque sua chave de API (veja *Primeiros passos*) e comece a conversar.

A Vercel entrega o app por HTTPS, então microfone, instalação e cache offline funcionam sem configuração.

### Opção 2 — Clonar ou baixar os arquivos e instalar no PC

1. Pegue os arquivos: clone o repositório, ou clique em **Code → Download ZIP** no GitHub e extraia.

   ```bash
   git clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
   cd SEU-REPOSITORIO
   ```

2. Confira se `index.html`, `manifest.json`, `sw.js` e os três arquivos `icon-*.png` estão na mesma pasta.
3. Inicie um servidor local nessa pasta (escolha um):

   ```bash
   python3 -m http.server 8000      # Linux / macOS (Windows: python -m http.server 8000)
   npx serve -l 8000                # alternativa, precisa do Node.js
   ```

4. Abra **http://localhost:8000** no Chrome e clique no ícone de instalar na barra de endereço (ou ⋮ → *Instalar Chat de IA*).
5. Coloque sua chave de API (veja *Primeiros passos*).

Observações para a Opção 2:
- Use sempre o **mesmo endereço e a mesma porta**. Suas conversas e configurações ficam ligadas a ele (`localhost:8000` e `localhost:8001` são apps diferentes, com dados separados).
- Depois de instalado, o app também abre com o servidor parado, graças ao cache. Para receber arquivos atualizados, inicie o servidor de novo e recarregue.
- Ao trocar os arquivos por uma versão nova, abra o app uma vez com o servidor rodando e depois feche e abra por completo, para o novo service worker assumir.

---

## ❓ Solução de problemas

- **O microfone não faz nada:** confira se está em HTTPS ou `localhost`, se a permissão de microfone está liberada para o site e se você usa Chrome ou Edge.
- **A fala é transcrita no idioma errado:** ajuste ⚙ → *Idioma da voz* para o idioma que você está falando. Ele não detecta o idioma sozinho.
- **Falta uma voz ou idioma para as respostas faladas:** as vozes vêm do seu aparelho. No Android, instale os dados de voz do idioma nas configurações de texto para fala do sistema.
- **A página aparece traduzida:** o app pede ao Chrome para não traduzir. Se o Chrome lembrou de uma tradução para o site, use ⋮ → *Mostrar original*.
- **A IA responde no idioma errado:** confira ⚙ → *Idioma das respostas da IA* e o texto da *Personalidade* (uma personalidade escrita em outro idioma puxa as respostas para ele; use *Restaurar padrão* para zerar). Teste numa conversa nova, pois respostas anteriores na mesma conversa também influenciam o idioma.
- **Um PDF é recusado:** o limite é de cerca de 14 MB. Divida ou comprima o arquivo.
- **Não suportado:** `.doc` antigo, `.xlsx`, `.pptx`, fotos HEIC e a exibição da resposta em tempo real (a resposta aparece quando está completa).
