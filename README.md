# 📚 Meu Diário de Professor de Física Digital - Versão Cloud

Sistema web 100% online para gestão de ensino de física, acessível de qualquer lugar!

## 🌐 Deploy Online GRATUITO

Este sistema pode ser hospedado **gratuitamente** e acessado de qualquer dispositivo com internet!

### 🚀 Opções de Hospedagem Gratuita

#### Opção 1: Firebase Hosting (RECOMENDADO) ⭐

**Vantagens:**
- Totalmente gratuito
- SSL/HTTPS automático
- CDN global
- Banco de dados incluído
- Autenticação incluída

**Passo a Passo:**

1. **Criar conta no Firebase**
   - Acesse: https://console.firebase.google.com/
   - Clique em "Adicionar projeto"
   - Nomeie: "diario-fisica"

2. **Configurar Authentication**
   - No console do Firebase, vá em "Authentication"
   - Clique em "Começar"
   - Ative "Email/Password"

3. **Configurar Firestore Database**
   - Vá em "Firestore Database"
   - Clique em "Criar banco de dados"
   - Escolha "Iniciar em modo de teste"
   - Selecione localização: "southamerica-east1"

4. **Configurar regras do Firestore**
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{userId} {
         allow read, write: if request.auth != null && request.auth.uid == userId;
       }
       match /questions/{questionId} {
         allow read, write: if request.auth != null && resource.data.userId == request.auth.uid;
       }
       match /lessonPlans/{planId} {
         allow read, write: if request.auth != null && resource.data.userId == request.auth.uid;
       }
       match /classes/{classId} {
         allow read, write: if request.auth != null && resource.data.userId == request.auth.uid;
       }
     }
   }
   ```

5. **Obter credenciais do Firebase**
   - Vá em "Configurações do projeto" (ícone de engrenagem)
   - Role até "Seus aplicativos"
   - Clique em "</>" (Web)
   - Registre o app: "diario-fisica-web"
   - Copie o código de configuração

6. **Atualizar app.js**
   - Abra `app.js`
   - Substitua `firebaseConfig` pelas suas credenciais:
   ```javascript
   const firebaseConfig = {
       apiKey: "SUA_API_KEY_AQUI",
       authDomain: "seu-projeto.firebaseapp.com",
       projectId: "seu-projeto-id",
       storageBucket: "seu-projeto.appspot.com",
       messagingSenderId: "123456789",
       appId: "sua-app-id"
   };
   ```

7. **Instalar Firebase CLI**
   ```bash
   npm install -g firebase-tools
   firebase login
   ```

8. **Inicializar e fazer deploy**
   ```bash
   # Na pasta do projeto
   firebase init hosting
   
   # Selecione:
   # - Use an existing project
   # - Seu projeto criado
   # - Public directory: . (ponto)
   # - Single-page app: Yes
   # - GitHub auto-deploys: No
   
   firebase deploy
   ```

9. **Pronto!** 🎉
   Seu site estará em: `https://seu-projeto.web.app`

---

#### Opção 2: GitHub Pages (Simples)

1. **Criar repositório no GitHub**
   - Vá em https://github.com/new
   - Nome: "diario-fisica"
   - Público
   - Crie o repositório

2. **Fazer upload dos arquivos**
   - Faça upload de: `index.html`, `styles.css`, `app.js`

3. **Ativar GitHub Pages**
   - Vá em Settings > Pages
   - Source: main branch
   - Salvar

4. **Configurar Firebase** (mesmo processo da Opção 1, passos 1-6)

5. **Acessar:** `https://seu-usuario.github.io/diario-fisica`

---

#### Opção 3: Netlify (Drop & Drop)

1. **Criar conta:** https://app.netlify.com/signup
2. **Arrastar a pasta** do projeto para o Netlify
3. **Configurar Firebase** (passos 1-6 da Opção 1)
4. **Pronto!** URL automática gerada

---

#### Opção 4: Vercel (Deploy Instantâneo)

1. **Criar conta:** https://vercel.com/signup
2. **Importar projeto** do GitHub ou fazer upload
3. **Configurar Firebase** (passos 1-6 da Opção 1)
4. **Deploy automático!**

---

## 📱 Acesso Multiplataforma

Após o deploy, você pode acessar de:
- ✅ Computador (qualquer navegador)
- ✅ Tablet
- ✅ Celular (iOS e Android)
- ✅ Qualquer lugar com internet!

## 🔒 Segurança

- ✅ Autenticação segura com Firebase
- ✅ HTTPS automático
- ✅ Dados isolados por usuário
- ✅ Regras de segurança no Firestore

## 🎯 Funcionalidades

### ✅ Implementadas
- **Autenticação** - Login e cadastro seguro
- **Banco de Questões** - CRUD completo
  - Múltiplas alternativas
  - Filtros por tópico e dificuldade
  - Organização por assunto
- **Planos de Aula** - Gestão completa
  - Objetivos, conteúdo, metodologia
  - Organização por data
- **Turmas** - Cadastro e gestão

### 🔜 Próximas Features
- Exportação de provas em PDF
- Sistema de simulados online
- Gráficos de desempenho
- Compartilhamento entre professores

## 💡 Dicas de Uso

1. **Primeiro Acesso**
   - Cadastre-se com seu email
   - Comece criando questões
   - Organize por tópicos desde o início

2. **Organização**
   - Use tags consistentes nos tópicos
   - Crie turmas antes de associar planos
   - Revise questões periodicamente

3. **Backup**
   - Seus dados ficam salvos no Firebase
   - Faça backup exportando periodicamente
   - Use o mesmo login em todos os dispositivos

## 🆘 Solução de Problemas

### Firebase não configurado
**Erro:** "Configure o Firebase primeiro!"
**Solução:** Siga os passos 1-6 da configuração do Firebase

### Não consigo fazer login
**Causa:** Authentication não ativado
**Solução:** No Firebase Console, ative Email/Password

### Dados não aparecem
**Causa:** Regras do Firestore muito restritivas
**Solução:** Configure as regras conforme o passo 4

### Erro ao salvar
**Causa:** Usuário sem permissão
**Solução:** Verifique se está logado e as regras do Firestore

## 📊 Estrutura de Dados (Firestore)

```
usuarios/
  └── {userId}
      ├── name
      ├── email
      └── createdAt

questions/
  └── {questionId}
      ├── statement
      ├── topic
      ├── difficulty
      ├── alternatives[]
      ├── userId
      └── createdAt

lessonPlans/
  └── {planId}
      ├── title
      ├── date
      ├── objectives
      ├── content
      ├── methodology
      ├── resources
      ├── userId
      └── createdAt

classes/
  └── {classId}
      ├── name
      ├── year
      ├── userId
      └── createdAt
```

## 🌟 Vantagens da Versão Cloud

### vs Versão Local
| Característica | Cloud | Local |
|---|---|---|
| Acesso de qualquer lugar | ✅ | ❌ |
| Sem instalação | ✅ | ❌ |
| Dados sincronizados | ✅ | ❌ |
| Backups automáticos | ✅ | ❌ |
| Multiplataforma | ✅ | ⚠️ |
| Gratuito | ✅ | ✅ |

## 🚀 Melhorias Futuras

1. **PWA** - Instalar como app no celular
2. **Offline** - Funcionar sem internet
3. **Colaboração** - Compartilhar com colegas
4. **Exportação** - PDF, Word, Excel
5. **Estatísticas** - Gráficos avançados
6. **Simulados** - Modo prova online
7. **Gamificação** - Ranking de alunos

## 📞 Suporte

**Problemas com Firebase?**
- Documentação: https://firebase.google.com/docs
- Console: https://console.firebase.google.com/

**Problemas com deploy?**
- Firebase Hosting: https://firebase.google.com/docs/hosting
- GitHub Pages: https://pages.github.com/
- Netlify: https://docs.netlify.com/
- Vercel: https://vercel.com/docs

## 📄 Arquivos do Projeto

```
diario-fisica-cloud/
├── index.html      # Interface completa
├── styles.css      # Estilos responsivos
├── app.js          # Lógica + Firebase
└── README.md       # Este arquivo
```

## ✨ Créditos

Sistema desenvolvido para professores de Física
Versão Cloud - Janeiro 2026

---

**🎓 Bom trabalho, professor!**

Agora você tem um sistema profissional, gratuito e acessível de qualquer lugar! 🚀
