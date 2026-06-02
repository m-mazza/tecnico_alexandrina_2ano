# Segurança em Aplicações: Conceitos Fundamentais

---

## O que é segurança em software?

Quando criamos uma aplicação — seja um site, um app ou um sistema —, precisamos proteger dois elementos principais: **os dados dos usuários** e **o acesso às funcionalidades**. Segurança não é um recurso extra; é uma responsabilidade desde o início do desenvolvimento.

---

## Conceito 1: Autenticação

**O que é?**
Autenticação é o processo de verificar *quem é* o usuário. É como mostrar um documento de identidade na entrada de um prédio.

**Exemplo do dia a dia:**
Quando você digita seu e-mail e senha para entrar em um sistema, está sendo *autenticado*.

**Métodos comuns:**
- Senha (algo que você sabe)
- Código enviado por SMS/e-mail — 2FA (algo que você recebe)
- Biometria: impressão digital, rosto (algo que você é)

**Por que importa?**
Sem autenticação, qualquer pessoa poderia acessar qualquer conta.

---

## Conceito 2: Autorização

**O que é?**
Autorização determina *o que* um usuário autenticado pode fazer. Duas pessoas podem entrar no mesmo sistema, mas com permissões diferentes.

**Diferença fundamental:**

| | Autenticação | Autorização |
|---|---|---|
| Pergunta | Quem é você? | O que você pode fazer? |
| Acontece | Antes | Depois da autenticação |
| Exemplo | Fazer login | Acessar o painel de administrador |

**Exemplo prático:**
Um funcionário e um gerente fazem login no mesmo sistema. O funcionário vê seu próprio histórico. O gerente vê o histórico de todos.

---

## Conceito 3: Roles (Papéis de Usuário)

**O que é?**
*Role* é o "papel" que um usuário desempenha no sistema. Em vez de definir permissões individualmente para cada pessoa, agrupamos usuários por função.

**Exemplo:**

```
Administrador → acesso total
Gerente       → acessa relatórios, mas não cria usuários
Usuário comum → acessa apenas o próprio perfil
```

**Por que usar roles?**
É muito mais fácil gerenciar. Se um gerente é promovido a administrador, basta mudar o papel — não é necessário alterar dezenas de permissões separadas.

---

## Conceito 4: Hashing de Senhas

**O que é?**
Hashing transforma uma senha em um código irreversível chamado *hash*. O sistema armazena o hash, nunca a senha original.

**Como funciona:**

```
Senha original:  "minhasenha123"
Após o hash:     "ef92b778bafe771207b..."  ← não dá para reverter
```

**Por que é importante?**
Se o banco de dados for invadido, o atacante encontrará apenas os hashes — inúteis sem a senha original. Armazenar senhas em texto puro é uma das falhas de segurança mais graves que existem.

**Analogia:**
É como guardar a impressão digital de alguém em vez da chave. Você consegue verificar se a chave bate, mas não consegue reconstruir a chave a partir da impressão.

---

## Conceito 5: Criptografia e HTTPS

**O que é criptografia?**
Criptografia embaralha os dados de forma que só quem tem a "chave" consegue ler. Sem criptografia, dados enviados pela internet podem ser interceptados.

**O que é HTTPS?**
É o protocolo que garante que a comunicação entre o navegador e o servidor seja criptografada. O "S" significa *Secure*.

**Como identificar:**
- `http://` → dados viajam sem proteção
- `https://` → dados viajam criptografados

**Por que importa?**
Em uma rede pública (café, aeroporto), sem HTTPS qualquer pessoa na mesma rede poderia ler os dados que você envia — incluindo senhas.

---

## Conceito 6: Token JWT

**O que é?**
JWT (JSON Web Token) é um "crachá digital" que o servidor entrega ao usuário após o login. Nas próximas requisições, o usuário apresenta esse token em vez de digitar a senha novamente.

**Como funciona:**

```
1. Usuário faz login com e-mail e senha
2. Servidor verifica as credenciais e gera um token
3. Usuário envia o token em cada requisição seguinte
4. Servidor valida o token e responde
```

**Analogia:**
Como um crachá de visitante em uma empresa. Você se identifica uma vez na recepção e depois usa o crachá para entrar nas áreas permitidas.

---

## Conceito 7: Validação de Entrada

**O que é?**
Toda informação que o usuário digita deve ser verificada antes de ser processada. Nunca confie no que vem do usuário.

**Por que?**
Um usuário mal-intencionado pode digitar comandos em vez de dados normais — isso é chamado de *injeção*. Se o sistema não validar a entrada, pode executar esses comandos sem querer.

**Exemplo simples:**

```
Campo de nome esperado: "João Silva"
O que um atacante pode tentar: "'; DELETE FROM usuarios; --"
```

Se o sistema aceitar esse segundo valor sem validar, pode apagar toda a tabela de usuários.

---

## Conceito 8: Logs e Auditoria

**O que é?**
Logs são registros de tudo que acontece no sistema: quem acessou, quando, o que fez, se houve falha.

**Para que servem?**
- Detectar tentativas de invasão
- Investigar problemas depois que acontecem
- Comprovar que o sistema está funcionando corretamente

**O que registrar:**
- Data e hora de cada acesso
- IP do usuário
- Ação realizada (login, alteração de dados, etc.)
- Se a ação foi bem-sucedida ou falhou

---
