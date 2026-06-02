# Atividade Prática — Sistema de Login com JavaScript Puro
---

## Objetivo

Construir, passo a passo, um sistema de login simples em HTML e JavaScript que demonstre na prática os conceitos de **autenticação**, **autorização** e **roles**.

---

## O que vamos construir

Um sistema com:
- Tela de login
- Três usuários com roles diferentes (admin, gerente, usuário)
- Painel que muda conforme o papel do usuário logado
- Mensagem de erro para credenciais inválidas

---

## Passo 1 — Criando a estrutura do arquivo

Crie um arquivo chamado `login.html` e cole o código abaixo. Este é o esqueleto da página.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Sistema de Login</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 500px;
      margin: 60px auto;
      padding: 20px;
    }
    input {
      display: block;
      width: 100%;
      margin: 8px 0;
      padding: 8px;
      box-sizing: border-box;
    }
    button {
      padding: 10px 20px;
      margin-top: 10px;
      cursor: pointer;
    }
    .erro {
      color: red;
    }
    .painel {
      display: none;
      border: 1px solid #ccc;
      padding: 20px;
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <h1>Sistema de Login</h1>

  <!-- Tela de login -->
  <div id="telaLogin">
    <label>E-mail:</label>
    <input type="email" id="email" placeholder="Digite seu e-mail">

    <label>Senha:</label>
    <input type="password" id="senha" placeholder="Digite sua senha">

    <button onclick="fazerLogin()">Entrar</button>
    <p class="erro" id="mensagemErro"></p>
  </div>

  <!-- Painel pós-login -->
  <div class="painel" id="painel">
    <p id="boasVindas"></p>
    <p>Seu papel: <strong id="roleUsuario"></strong></p>
    <div id="conteudoPainel"></div>
    <button onclick="fazerLogout()">Sair</button>
  </div>

  <script src="login.js"></script>
</body>
</html>
```

**Pause aqui.** Abra o arquivo no navegador. O que você vê? A tela de login deve aparecer, mas o botão ainda não faz nada.

---

## Passo 2 — Criando os usuários

Crie um arquivo chamado `login.js` na mesma pasta. Este arquivo conterá toda a lógica do sistema.

```javascript
// Passo 2: Nosso "banco de dados" de usuários
// Em um sistema real, isso estaria em um servidor — nunca no navegador.
// Aqui usamos um array só para aprender os conceitos.

const usuarios = [
  {
    email: "admin@empresa.com",
    senha: "admin123",
    nome: "Ana Administradora",
    role: "administrador"
  },
  {
    email: "gerente@empresa.com",
    senha: "gerente123",
    nome: "Bruno Gerente",
    role: "gerente"
  },
  {
    email: "usuario@empresa.com",
    senha: "usuario123",
    nome: "Carlos Usuário",
    role: "usuario"
  }
];
```

**Ponto de atenção:** Perceba que as senhas estão em texto puro. Isso é um problema de segurança — faremos melhor no Passo 5.

---

## Passo 3 — Implementando a autenticação

Adicione a função de login ao arquivo `login.js`:

```javascript
// Passo 3: Função de autenticação
function fazerLogin() {
  // 1. Pegar o que o usuário digitou
  const emailDigitado = document.getElementById("email").value;
  const senhaDigitada = document.getElementById("senha").value;

  // 2. Procurar o usuário no array
  const usuarioEncontrado = usuarios.find(function(u) {
    return u.email === emailDigitado && u.senha === senhaDigitada;
  });

  // 3. Se encontrou: autenticação bem-sucedida
  if (usuarioEncontrado) {
    document.getElementById("mensagemErro").textContent = "";
    mostrarPainel(usuarioEncontrado);
  } else {
    // 4. Se não encontrou: mostrar erro
    document.getElementById("mensagemErro").textContent =
      "E-mail ou senha incorretos.";
  }
}
```

**Teste agora:** Tente fazer login com `admin@empresa.com` e `admin123`. Ainda não verá o painel — vamos criar no próximo passo.

---

## Passo 4 — Implementando a autorização por role

Adicione as funções de painel e logout ao `login.js`:

```javascript
// Passo 4: Autorização — o que cada role pode ver
function mostrarPainel(usuario) {
  // Esconder tela de login
  document.getElementById("telaLogin").style.display = "none";

  // Mostrar painel
  document.getElementById("painel").style.display = "block";
  document.getElementById("boasVindas").textContent =
    "Bem-vindo(a), " + usuario.nome + "!";
  document.getElementById("roleUsuario").textContent = usuario.role;

  // Conteúdo muda conforme o role
  const areaConteudo = document.getElementById("conteudoPainel");

  if (usuario.role === "administrador") {
    areaConteudo.innerHTML = `
      <h3>Painel do Administrador</h3>
      <p>✅ Gerenciar usuários</p>
      <p>✅ Ver todos os relatórios</p>
      <p>✅ Configurações do sistema</p>
    `;
  } else if (usuario.role === "gerente") {
    areaConteudo.innerHTML = `
      <h3>Painel do Gerente</h3>
      <p>✅ Ver relatórios</p>
      <p>✅ Gerenciar equipe</p>
      <p>❌ Configurações do sistema (sem permissão)</p>
    `;
  } else {
    areaConteudo.innerHTML = `
      <h3>Painel do Usuário</h3>
      <p>✅ Ver seu perfil</p>
      <p>❌ Relatórios (sem permissão)</p>
      <p>❌ Configurações do sistema (sem permissão)</p>
    `;
  }
}

// Logout
function fazerLogout() {
  document.getElementById("telaLogin").style.display = "block";
  document.getElementById("painel").style.display = "none";
  document.getElementById("email").value = "";
  document.getElementById("senha").value = "";
  document.getElementById("conteudoPainel").innerHTML = "";
}
```

**Teste agora:** Faça login com os três usuários diferentes e observe como o painel muda.

---

## Passo 5 — Simulando o hashing de senhas

No Passo 2 as senhas estavam em texto puro — um problema grave. Vamos simular como o hashing funciona. Substitua o array `usuarios` no início do `login.js`:

```javascript
// Passo 5: Senhas "hasheadas" (simulação didática)
// Em um sistema real, o hash seria gerado com bcrypt ou similar no servidor.
// Aqui usamos uma função simples só para ilustrar o conceito.

function hashSimples(texto) {
  // Simulação: transforma cada letra em seu código numérico e embaralha
  // ATENÇÃO: isso NÃO é seguro para uso real — é apenas para visualizar o conceito
  let resultado = 0;
  for (let i = 0; i < texto.length; i++) {
    resultado = (resultado * 31 + texto.charCodeAt(i)) % 1000000007;
  }
  return "hash_" + resultado.toString(16);
}

// Agora os usuários armazenam apenas o hash, não a senha real
const usuarios = [
  {
    email: "admin@empresa.com",
    senhaHash: hashSimples("admin123"),
    nome: "Ana Administradora",
    role: "administrador"
  },
  {
    email: "gerente@empresa.com",
    senhaHash: hashSimples("gerente123"),
    nome: "Bruno Gerente",
    role: "gerente"
  },
  {
    email: "usuario@empresa.com",
    senhaHash: hashSimples("usuario123"),
    nome: "Carlos Usuário",
    role: "usuario"
  }
];
```

E atualize a função `fazerLogin` para comparar com o hash:

```javascript
// Função de login atualizada para usar hashing
function fazerLogin() {
  const emailDigitado = document.getElementById("email").value;
  const senhaDigitada = document.getElementById("senha").value;

  // Gerar o hash da senha digitada para comparar
  const hashDaSenhaDigitada = hashSimples(senhaDigitada);

  // Comparar com o hash armazenado — nunca com a senha original
  const usuarioEncontrado = usuarios.find(function(u) {
    return u.email === emailDigitado && u.senhaHash === hashDaSenhaDigitada;
  });

  if (usuarioEncontrado) {
    document.getElementById("mensagemErro").textContent = "";
    mostrarPainel(usuarioEncontrado);
  } else {
    document.getElementById("mensagemErro").textContent =
      "E-mail ou senha incorretos.";
  }
}
```

**Ponto de reflexão:** Abra o console do navegador (F12 → Console) e digite `usuarios`. O que você vê? As senhas aparecem ou apenas os hashes?

---

## Passo 6 — Adicionando log de tentativas

Para fechar o ciclo, vamos registrar as tentativas de login. Adicione ao `login.js`:

```javascript
// Passo 6: Log de auditoria (registrado no console do navegador)
const logAcessos = [];

function registrarLog(email, sucesso) {
  const registro = {
    horario: new Date().toLocaleString("pt-BR"),
    email: email,
    resultado: sucesso ? "LOGIN BEM-SUCEDIDO" : "FALHA NO LOGIN"
  };

  logAcessos.push(registro);
  console.log("[LOG]", registro);
}
```

E adicione a chamada `registrarLog` dentro da função `fazerLogin`:

```javascript
// Dentro do if/else da função fazerLogin, adicione:
if (usuarioEncontrado) {
  registrarLog(emailDigitado, true);   // ← adicionar esta linha
  document.getElementById("mensagemErro").textContent = "";
  mostrarPainel(usuarioEncontrado);
} else {
  registrarLog(emailDigitado, false);  // ← adicionar esta linha
  document.getElementById("mensagemErro").textContent =
    "E-mail ou senha incorretos.";
}
```

**Teste:** Abra o console (F12) e faça algumas tentativas — certas e erradas. Veja os logs sendo registrados em tempo real.

---

## Perguntas para discussão em sala

1. No Passo 2, as senhas estavam em texto puro. Por que isso é um problema grave mesmo que o arquivo fique "escondido"?

2. No Passo 4, o painel do gerente mostra `❌ Configurações do sistema (sem permissão)`. No código, o que impede de fato o gerente de acessar? É só a mensagem visual ou há outra proteção?

3. A função `hashSimples` do Passo 5 é suficiente para uso em produção? Por que não?

4. O log do Passo 6 está no console do navegador. Quem pode ver esse log? Onde deveria estar em um sistema real?

5. O que aconteceria se um usuário editasse o HTML no navegador e mudasse seu próprio `role` para "administrador"? Como isso poderia ser prevenido?

---

## Conexão com os conceitos teóricos

| Conceito | Onde aparece na atividade |
|---|---|
| Autenticação | Função `fazerLogin` — verificar e-mail e hash da senha |
| Autorização | Função `mostrarPainel` — conteúdo diferente por role |
| Roles | Array `usuarios` com campo `role` |
| Hashing | Função `hashSimples` e comparação de hash no login |
| Logs e auditoria | Array `logAcessos` e função `registrarLog` |
| Validação de entrada | Perguntas 2 e 5 apontam para essa lacuna — próxima aula |

---

