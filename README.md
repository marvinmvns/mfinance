# M Finance

**Terminal financeiro local e offline.** Dashboard, transações, faturas, planejamento mensal, alertas e assistente de IA — tudo rodando na sua máquina, com banco de dados local (nada vai pra nuvem). Conecta nos seus dados via [Pierre Open Finance](https://pierre.finance).

> Este repositório contém **apenas os instaladores** (binários) para download. O código-fonte não fica aqui.

---

## ⬇️ Download

Baixe o instalador do seu sistema na página de **[Releases](https://github.com/marvinmvns/mfinance/releases/latest)**:

| Sistema | Arquivo | Tamanho |
| --- | --- | --- |
| **Windows** 10/11 (x64) | [`MFinance-Setup-0.1.0.exe`](https://github.com/marvinmvns/mfinance/releases/download/v0.1.0/MFinance-Setup-0.1.0.exe) | ~213 MB |
| **Linux** (AppImage, qualquer distro) | [`MFinance-0.1.0.AppImage`](https://github.com/marvinmvns/mfinance/releases/download/v0.1.0/MFinance-0.1.0.AppImage) | ~270 MB |
| **Linux** (Debian/Ubuntu, `.deb`) | [`mfinance_0.1.0_amd64.deb`](https://github.com/marvinmvns/mfinance/releases/download/v0.1.0/mfinance_0.1.0_amd64.deb) | ~163 MB |

> **macOS:** ainda não há instalador `.dmg` pronto (precisa ser gerado em um Mac). Em breve.

Os instaladores são **self-contained**: já trazem tudo embutido (runtime, servidor e banco). Não precisa instalar Node, Docker nem nada.

---

## 🪟 Windows

1. Baixe o **`MFinance-Setup-0.1.0.exe`**.
2. Dê duplo-clique para instalar. Pode escolher a pasta de instalação.
3. O app **não é assinado digitalmente**, então o **Windows SmartScreen** pode avisar "Windows protegeu o computador". Clique em **"Mais informações" → "Executar assim mesmo"**.
4. Abra **M Finance** pelo menu Iniciar.

## 🐧 Linux — AppImage (qualquer distribuição)

```bash
chmod +x MFinance-0.1.0.AppImage
./MFinance-0.1.0.AppImage
```

> Se aparecer erro de sandbox (`SUID sandbox`), rode com:
> ```bash
> ./MFinance-0.1.0.AppImage --no-sandbox
> ```

## 🐧 Linux — Debian / Ubuntu (`.deb`)

```bash
sudo apt install ./mfinance_0.1.0_amd64.deb
# depois é só procurar "M Finance" no menu de aplicativos, ou:
mfinance
```

---

## 🚀 Primeiro uso

1. Ao abrir pela primeira vez, o app mostra um **assistente de configuração** (`/setup`).
2. Você vai precisar de uma **chave de API da Pierre** — gere em <https://pierre.finance/api-key>.
3. Cole a chave, conecte suas contas e clique em **"Iniciar sincronização"**. O app baixa suas contas, transações e faturas para o banco local.
4. Pronto — dashboard, planejamento, alertas e o assistente de IA já ficam disponíveis.

Tudo funciona **offline** depois do sync: os dados ficam no seu computador, e novas sincronizações só acontecem quando você pede.

---

## 💾 Onde ficam os dados

O banco de dados local (e a chave-mestra de criptografia) ficam por usuário:

| Sistema | Pasta |
| --- | --- |
| Windows | `%APPDATA%\openfinance-desktop\` |
| Linux | `~/.config/openfinance-desktop/` |

Para **fazer backup**, copie o `openfinance.db` (e o `.master-key`) dessa pasta.
Para **resetar** o app do zero, feche-o e apague essa pasta.

---

## ❓ Problemas comuns

- **"Falha: invalid fts5 file format"** no sync — corrigido nesta versão: o índice de busca se auto-repara no boot. Se persistir em um banco muito antigo, feche o app e apague a pasta de dados acima para começar limpo.
- **SmartScreen (Windows) / "app não verificado"** — esperado, pois o instalador não é assinado. Veja o passo 3 do Windows acima.
- **App não abre no Linux** — tente rodar pelo terminal com `--no-sandbox` para ver mensagens de erro.

---

## 🔒 Privacidade

100% local. Seus dados financeiros ficam no **seu** computador, em um banco SQLite com segredos criptografados (AES-256-GCM). Nenhum dado é enviado para servidores de terceiros além das chamadas que **você** autoriza à API da Pierre durante a sincronização.

---

_M Finance v0.1.0_
