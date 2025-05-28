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

### ✅ **Etapa 4: Salvar o arquivo de configuração na NVRAM**

**Pergunta:**
**Qual comando você emite para executar esta etapa?**

**Resposta objetiva:**

```bash
copy running-config startup-config
```

> Esse comando salva a configuração atual (em RAM) na NVRAM, garantindo que seja mantida após o reinício do equipamento.

### ✅ **Parte 2: Configurar os PCs**

---

### 🔹 **Etapa 1: Configurar IPs em PC1 e PC2**

**Para PC1:**

1. Clique em **PC1**.
2. Vá na aba **Desktop**.
3. Clique em **IP Configuration**.
4. Insira:

   * **IP Address**: `192.168.1.1`
   * **Subnet Mask**: `255.255.255.0`

**Para PC2:**

1. Clique em **PC2**.
2. Vá na aba **Desktop**.
3. Clique em **IP Configuration**.
4. Insira:

   * **IP Address**: `192.168.1.2`
   * **Subnet Mask**: `255.255.255.0`

---

### 🔹 **Etapa 2: Testar a conectividade com o switch S1**

1. No **PC1**, clique na aba **Desktop > Command Prompt**.
2. Digite:

```bash
ping 192.168.1.253
```

---

### ❓ **Pergunta: Deu certo? Explique.**

**Resposta:**

**Depende.** O comando `ping 192.168.1.253` só funcionará se **S1 tiver um endereço IP configurado na VLAN 1 (ou na VLAN correta)** com o IP `192.168.1.253`.

---

### 🔍 **Verificação no switch S1:**

Você precisa ter executado este comando no S1 anteriormente:

```bash
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.253 255.255.255.0
S1(config-if)# no shutdown
```

E S1 deve estar **conectado via cabo ao PC1** em portas ativas.

---

### ✅ **Se tudo estiver correto:**

* O ping funcionará e mostrará:

```
Reply from 192.168.1.253: bytes=32 time<1ms TTL=255
```

### ❌ **Se não funcionar:**

* Você verá:

```
Request timed out.
```

---

Segue a explicação **detalhada e objetiva**, conforme solicitado, da **Parte 3 – Configurar a interface de gerenciamento do switch**, com todas as etapas, respostas às perguntas e comandos:

---

### ✅ **Etapa 1: Configurar o S1 com um endereço IP**

**Comandos usados:**

```bash
S1# configure terminal
S1(config)# interface vlan 1
S1(config-if)# ip address 192.168.1.253 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
S1(config)# exit
```

---

### ❓ **Pergunta: Por que configurar o switch com um endereço IP?**

**Resposta:**
Porque o IP permite o **gerenciamento remoto** do switch via **telnet, SSH ou SNMP**, já que switches Layer 2 não atribuem IPs às portas físicas, mas sim à **interface VLAN de gerenciamento**.

---

### ❓ **Pergunta: Por que inserir o comando `no shutdown`?**

**Resposta:**
Porque a interface VLAN 1 vem desativada por padrão. O comando `no shutdown` **ativa a interface**, permitindo a comunicação IP com o switch.

---

### ✅ **Etapa 2: Configurar o S2 com um endereço IP**

**Exemplo (supondo IP 192.168.1.254 para S2):**

```bash
S2# configure terminal
S2(config)# interface vlan 1
S2(config-if)# ip address 192.168.1.254 255.255.255.0
S2(config-if)# no shutdown
S2(config-if)# exit
S2(config)# exit
```

---

### ✅ **Etapa 3: Verificar a configuração IP em S1 e S2**

**Comandos úteis:**

```bash
S1# show ip interface brief
```

**Verifique:**

* Interface VLAN 1 com IP correto
* Status como **up** e **up**

Também pode usar:

```bash
S1# show running-config
```

---

### ✅ **Etapa 4: Salvar configurações na NVRAM**

**Pergunta: Qual comando é usado?**

**Resposta:**

```bash
copy running-config startup-config
```

---

### ✅ **Etapa 5: Verificar a conectividade da rede**

**No PC1:**

1. Vá em **Desktop > Command Prompt**
2. Execute os comandos:

```bash
ping 192.168.1.2      // Ping para o PC2
ping 192.168.1.253    // Ping para o S1
ping 192.168.1.254    // Ping para o S2
```

**Observação:**

* Se o primeiro ping falhar parcialmente (ex: 80%), isso pode ocorrer porque a **tabela ARP** ainda não foi atualizada. Tente novamente para obter 100%.
* Se o ping **falhar completamente**, revise as configurações de IP, cabos e VLANs.

---

