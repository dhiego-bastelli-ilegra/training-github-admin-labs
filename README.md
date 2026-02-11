# 📦 Repository Template – Secure by Default

Este repositório segue boas práticas de **segurança, governança e DevSecOps**, garantindo que código sensível não seja versionado acidentalmente e que todos os colaboradores trabalhem sob os mesmos padrões.

---

## 🎯 Objetivos

- Prevenir o commit de **dados sensíveis (secrets, tokens, chaves, senhas)**
- Padronizar o uso de **hooks pré-commit**
- Garantir segurança **local (shift-left)** e **no CI/CD**
- Facilitar o onboarding de novos colaboradores
- Atender requisitos de **auditoria e compliance**

---

## 🔐 Segurança – Visão Geral

Este repositório utiliza:

- **pre-commit** → framework de hooks locais
- **gitleaks** → detecção de secrets
- **GitHub Actions** → verificação adicional no CI
- **SECURITY.md** → política de reporte de vulnerabilidades

A segurança é aplicada em **múltiplas camadas**:

1. 💻 Antes do commit (máquina do desenvolvedor)
2. 🔁 Durante Pull Requests
3. 🚀 Durante pushes para branches protegidas

---

## 🧰 Pré-requisitos

- Git
- Python 3.8+ (recomendado)
- Acesso ao repositório

---

## 🚀 Onboarding rápido (obrigatório)

### 1️⃣ Clonar o repositório

```bash
git clone <URL_DO_REPOSITORIO>
cd <NOME_DO_REPOSITORIO>
````

---

### 2️⃣ Instalar o `pre-commit`

#### 🐧 Linux

```bash
python3 -m pip install --user pre-commit
```

ou

```bash
sudo apt install pre-commit
```

---

#### 🍎 macOS

```bash
brew install pre-commit
```

---

#### 🪟 Windows

```powershell
python -m pip install pre-commit
```

> ⚠️ No Windows, os hooks são executados via **Git Bash** (gerenciado automaticamente pelo `pre-commit`).

---

### 3️⃣ Ativar os hooks (passo essencial)

```bash
pre-commit install
```

Isso cria automaticamente o hook em:

```text
.git/hooks/pre-commit
```

A partir desse momento, **todo commit será validado automaticamente**.

---

## 🔎 O que acontece durante um commit

Quando você executa:

```bash
git commit -m "mensagem"
```

O sistema:

1. Executa o hook pré-commit
2. Roda o **gitleaks** nos arquivos staged
3. ❌ Bloqueia o commit se encontrar dados sensíveis
4. ✅ Permite o commit se tudo estiver seguro

---

## 🛡️ CI/CD – Camada adicional de segurança

Mesmo que o hook local não seja instalado, o repositório possui verificação automática no **CI/CD**:

* Pull Requests
* Push para `main`
* Branches protegidas

Isso garante que **nenhum secret chegue ao repositório remoto**.

---

## 📁 Estrutura relevante do repositório

```text
.
├── .github/
│   └── workflows/
│       └── gitleaks.yml
├── .pre-commit-config.yaml
├── SECURITY.md
├── README.md
```

---

## 🔧 Customização de regras (quando aplicável)

Atualmente, o projeto utiliza **as regras padrão do gitleaks**.

Regras customizadas só devem ser adicionadas se:

* Existirem tokens internos com padrão próprio
* Houver alto volume de falsos positivos
* For exigência de compliance

Qualquer customização deve ser:

* Versionada
* Documentada
* Aprovada pelo time responsável por segurança

---

## 📜 Política de Segurança

Consulte o arquivo [`SECURITY.md`](./SECURITY.md) para instruções sobre:

* Reporte responsável de vulnerabilidades
* Canais oficiais de contato
* Boas práticas de disclosure

---

## 📋 Boas práticas obrigatórias

* ❌ Nunca commitar secrets
* ❌ Nunca burlar hooks
* ✅ Utilizar Secret Managers
* ✅ Usar Pull Requests
* ✅ Respeitar branch protection rules

---

## 🧪 Solução de problemas

### O hook não está rodando

Verifique:

```bash
pre-commit --version
ls .git/hooks/pre-commit
```

Reinstale se necessário:

```bash
pre-commit install --force
```

---

## 📌 Observações finais

* Hooks locais **não substituem** pipelines
* Segurança é responsabilidade de todos
* Em caso de dúvida, **não commite**

---
