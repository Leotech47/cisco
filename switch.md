A seguir, explico detalhadamente e passo a passo como realizar a configuração básica em switches Cisco (S1 e S2), utilizando a interface de linha de comando (CLI):

---

### ✅ **Parte 1: Configuração básica no S1 e S2**

---

### 🔹 **Etapa 1: Configurar o nome do host**

**Objetivo:** Alterar o nome do dispositivo para "S1" (ou "S2" no segundo switch).

**Passos:**

1. Clique no switch (ex: S1).
2. Vá para a aba **CLI**.
3. Digite os comandos abaixo:

```bash
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
```

> Resultado: o prompt mudará de `Switch(config)#` para `S1(config)#`, indicando que o nome foi alterado com sucesso.

> **No S2**, substitua `S1` por `S2`.

---

### 🔹 **Etapa 2: Configurar senhas e acesso**

#### **a. Senha do console: `cisco`**

```bash
S1(config)# line console 0
S1(config-line)# password cisco
S1(config-line)# login
S1(config-line)# exit
```

#### **b. Senha do modo EXEC privilegiado: `class` (criptografada)**

```bash
S1(config)# enable secret class
```

#### **c. Habilitar criptografia de senhas do tipo `password`**

```bash
S1(config)# service password-encryption
```

---

### 🔹 **Etapa 3: Verificar se as senhas foram configuradas corretamente**

**Comando para verificar:**

```bash
S1# show running-config
```

**Verifique:**

* Se há a linha: `enable secret 5 <senha criptografada>`
* Se há: `line console 0` seguido de `password 7 <senha criptografada>` e `login`

> Isso confirma que ambas as senhas estão configuradas e criptografadas.

---

### 🔹 **Etapa 4: Configurar o banner de aviso**

**Comando:**

```bash
S1(config)# banner motd #Somente Acesso Autorizado. Infratores sofrerão as consequências da lei.#
```

> O caractere `#` delimita o início e o fim do texto do banner. Você pode usar outro caractere que **não apareça no texto**.

---

### ✅ Resultado Esperado:

Ao final, você deve ver no `show running-config`:

* Nome do host alterado
* Senhas configuradas e criptografadas
* Banner configurado
* Senha de console ativa

---

