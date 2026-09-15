# Configuração do Firebase — passo a passo

## 1. Criar o projeto
1. Acesse https://console.firebase.google.com
2. "Adicionar projeto" → dê um nome → pode desativar o Google Analytics (opcional)

## 2. Ativar Authentication (login anônimo)
1. Menu lateral → **Compilação** → **Authentication** → "Vamos começar"
2. Aba "Método de login" → ative **Anônimo**

## 3. Ativar Firestore Database
1. Menu lateral → **Compilação** → **Firestore Database** → "Criar banco de dados"
2. Escolha "Modo de produção" e a região (ex: `southamerica-east1` para São Paulo)
3. Vá em **Regras** (aba no topo) → cole o conteúdo do arquivo `firestore.rules` → **Publicar**

> Este projeto **não usa o Firebase Storage** (que hoje exige cartão de crédito / plano Blaze).
> A foto vai comprimida e gravada como texto (base64) direto dentro do documento do
> Firestore, que continua 100% gratuito, sem cartão. O limite é de ~1 MB por foto
> (o app já compacta a imagem automaticamente para caber nesse limite).

## 4. Criar o app Web e copiar as credenciais
1. Página inicial do projeto → ícone **`</>`** (Web)
2. Dê um nome ao app → "Registrar app"
3. Copie o objeto `firebaseConfig` mostrado na tela
4. Abra o arquivo `firebase-config.js` deste projeto e substitua os valores de exemplo

## 5. Ajustar o link do QR Code
No mesmo `firebase-config.js`, edite a linha:
```js
const VERIFY_BASE_URL = "https://SEU-USUARIO.github.io/SEU-REPOSITORIO/verify.html";
```
Coloque o endereço real onde o `verify.html` vai ficar publicado (o mesmo domínio do GitHub Pages).

## 6. Publicar no GitHub Pages
Suba todos os arquivos desta pasta (mantendo a estrutura) para um repositório e ative o GitHub Pages nas configurações do repositório.

## Sobre o CPF
O CPF digitado no app **não aparece na página de validação (QR Code)** — ele é gravado numa coleção separada (`fotos_privado`) que as regras do Firestore bloqueiam para leitura pelo próprio app. Só é visível para quem tiver acesso ao painel do Firebase (Firestore Database → coleção `fotos_privado`), pensado para auditoria interna.

Vale revisar com o time jurídico/compliance se a coleta de CPF neste fluxo tem base legal adequada (LGPD), já que é dado pessoal sensível de identificação.
