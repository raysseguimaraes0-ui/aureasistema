# Livro de Imóveis — Painel da Auréa Guimarães

Dashboard de gestão imobiliária: imóveis, locadores, locatários, financeiro,
cartão de crédito, ocorrências e calendário de vencimentos.

## 1. Criar o banco de dados (Supabase)

1. Crie uma conta grátis em https://supabase.com
2. Crie um novo projeto (anote a senha do banco que você definir)
3. No menu lateral, vá em **SQL Editor → New query**
4. Cole o conteúdo do arquivo `supabase-setup.sql` (está nesta mesma pasta) e clique em **Run**
5. Vá em **Project Settings → API** e copie dois valores:
   - **Project URL**
   - **anon public** (a chave pública)

## 2. Configurar o arquivo

Abra `dashboard-imoveis-supabase.html` em um editor de texto e localize estas
duas linhas, perto do início do `<script>`:

```js
const SUPABASE_URL = 'COLOQUE_AQUI_SUA_PROJECT_URL';
const SUPABASE_ANON_KEY = 'COLOQUE_AQUI_SUA_ANON_KEY';
```

Substitua pelos valores que você copiou no passo 1. Salve o arquivo.

> Se você abrir o painel sem preencher essas linhas, a tela de login vai
> mostrar um aviso de "Configuração pendente" em vez de travar sem explicação.

## 3. Subir para o GitHub

```bash
git init
git add dashboard-imoveis-supabase.html
git commit -m "Painel inicial"
git branch -M main
git remote add origin <URL_DO_SEU_REPOSITORIO>
git push -u origin main
```

Renomeie o arquivo para `index.html` antes de subir (ou configure o Render
para servir `dashboard-imoveis-supabase.html` como página inicial — ver passo 4).

## 4. Publicar no Render

1. No Render, clique em **New → Static Site**
2. Conecte o repositório do GitHub que você acabou de criar
3. Configurações:
   - **Build Command:** deixe em branco (não há build, é HTML puro)
   - **Publish Directory:** `.` (raiz do repositório)
4. Clique em **Create Static Site**

Em poucos minutos o Render te dá uma URL pública (tipo
`https://seu-app.onrender.com`) — é esse link que a Auréa vai usar no
celular e no notebook. Como os dados agora ficam no Supabase (não mais
presos a uma conversa do Claude), os dois aparelhos vão ver as mesmas
informações automaticamente.

## Acesso ao painel

- **Usuário:** Aurea
- **Senha:** aurea@2026!

(Isso é criado automaticamente no banco na primeira vez que alguém abrir o
painel. Pode ser trocado a qualquer momento pelo link "Esqueci o usuário ou
a senha" na tela de login.)

## Importante sobre segurança

A tela de login do painel é uma trava de **interface**, não uma autenticação
real como a de um banco ou e-mail. A política do banco (`supabase-setup.sql`)
libera leitura/escrita para quem tiver a URL + a chave pública do projeto,
que ficam visíveis no próprio HTML. Para um painel de uso pessoal/familiar
isso costuma ser aceitável, mas não é adequado para dados extremamente
sensíveis ou de terceiros com expectativa de confidencialidade forte. Se
esse for o caso no futuro, vale migrar para autenticação real do Supabase
(Supabase Auth) — é um passo a mais que também posso te ajudar a fazer.
