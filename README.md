# M Finance

Um aplicativo de finanças pessoais que roda **inteiro na sua máquina**. Ele conecta nas suas contas e cartões através do [Pierre Open Finance](https://pierre.finance), baixa tudo para um banco de dados local e te dá um painel completo: saldos, extrato, faturas, planejamento do mês, alertas e até um assistente que responde perguntas sobre o seu dinheiro.

A ideia é simples: depois da primeira sincronização, os seus dados financeiros ficam **no seu computador**, não numa nuvem de terceiros. Nada de mensalidade, nada de servidor remoto guardando o seu extrato.

> Este repositório serve **só para baixar o programa**. O código-fonte mora em outro lugar — aqui ficam apenas os instaladores.

---

## O que dá pra fazer

### Visão geral do seu dinheiro
Logo na tela inicial você vê o **patrimônio líquido** (somando contas e investimentos, descontando o que deve no cartão e em empréstimos) e o **fluxo de caixa dos últimos 30 dias** — quanto entrou, quanto saiu. Dá pra ligar e desligar cada bloco do painel e até montar mais de um painel, cada um com os módulos que te interessam. Transferências entre as suas próprias contas não entram na conta de "gastos", então o número não fica inflado.

### Contas e patrimônio
Todas as contas conectadas num lugar só, com o saldo de cada uma e a evolução ao longo do tempo (o app guarda um histórico a cada sincronização, mesmo que o banco não forneça isso). Você decide o que entra ou não no cálculo do patrimônio — por exemplo, esconder um empréstimo ou destacar só o que tem em conta.

### Extrato e transações
O extrato completo com filtros por período, conta, categoria, tipo, status e **faixa de valor**, além de busca por texto ("aquela compra no mercado"). Cada lançamento pode ser **recategorizado** com um clique, e o app aprende com isso: se você corrige o mesmo tipo de gasto várias vezes, ele sugere criar uma regra automática. Dá pra exportar tudo em CSV.

### Faturas e cartões
Uma área dedicada ao cartão de crédito, separando bem três coisas que costumam se misturar: as **faturas** em si (em aberto, a vencer e o histórico mês a mês), as **compras** feitas no cartão e os **pagamentos** de fatura saindo da conta. Inclui também o acompanhamento de **compras parceladas**, mostrando quanto já foi pago e quanto ainda falta.

### Planejamento mensal
Aqui você define o que espera receber e gastar no mês — salário, aluguel, assinaturas, uma reserva — e o app casa automaticamente cada item com as transações reais conforme elas chegam, mostrando se você está dentro ou fora do previsto. Um assistente ajuda a classificar gastos recorrentes em lote, e um calendário projeta o seu fluxo de caixa para os próximos 30 dias.

### Alertas
Você configura avisos para as situações que importam e o app fica de olho sozinho. Alguns exemplos do que ele consegue monitorar: saldo baixo, gasto numa categoria passando de um limite, fatura perto de vencer, uso alto do limite do cartão, salário que caiu na conta, uma entrada fora do comum, um Pix para um destino novo. Cada alerta tem um intervalo mínimo entre avisos para não virar spam, e os disparos podem chegar no Telegram com botões de ação rápida (ver detalhes, conversar com o assistente, silenciar por 24h).

### Assistente com IA
Um chat onde você pergunta em português sobre as suas finanças — *"quanto gastei com delivery esse mês?"*, *"quando começou minha assinatura da Netflix?"* — e o assistente consulta os seus dados para responder. Ele também entende pedidos como *"me avisa quando eu passar de R$ 500 com Uber no mês"* e cria o alerta sozinho. É opcional e funciona com diferentes provedores de IA.

### Telegram
Se quiser, dá pra conversar com o assistente e receber os alertas direto pelo Telegram, sem precisar abrir o programa — útil para uma consulta rápida de saldo ou para forçar uma sincronização de qualquer lugar.

### Aparência
Vários temas prontos (do "terminal preto" clássico a esquemas claros e coloridos) e uma interface que se adapta bem ao celular.

---

## Como funciona, por baixo

Tudo é **offline depois do sync**. O programa sobe um pequeno servidor local, guarda seus dados num banco SQLite na sua máquina e só fala com a internet quando **você** pede uma nova sincronização com a Pierre. Os instaladores já trazem tudo embutido — não precisa instalar Node, Docker ou qualquer dependência. É só baixar e abrir.

---

## ⬇️ Download

Baixe o instalador do seu sistema na página de **[Releases](https://github.com/marvinmvns/mfinance/releases/latest)**:

| Sistema | Arquivo | Tamanho |
| --- | --- | --- |
| **Windows** 10/11 (x64) | [`MFinance-Setup-0.1.0.exe`](https://github.com/marvinmvns/mfinance/releases/download/v0.1.0/MFinance-Setup-0.1.0.exe) | ~213 MB |
| **Linux** (AppImage, qualquer distro) | [`MFinance-0.1.0.AppImage`](https://github.com/marvinmvns/mfinance/releases/download/v0.1.0/MFinance-0.1.0.AppImage) | ~270 MB |
| **Linux** (Debian/Ubuntu, `.deb`) | [`mfinance_0.1.0_amd64.deb`](https://github.com/marvinmvns/mfinance/releases/download/v0.1.0/mfinance_0.1.0_amd64.deb) | ~163 MB |

> **macOS:** ainda não há instalador `.dmg` pronto (precisa ser gerado em um Mac). Em breve.

---

## 🪟 Windows

1. Baixe o **`MFinance-Setup-0.1.0.exe`**.
2. Dê duplo-clique para instalar. Pode escolher a pasta de instalação.
3. Como o app **não é assinado digitalmente**, o **Windows SmartScreen** pode mostrar "Windows protegeu o computador". Clique em **"Mais informações" → "Executar assim mesmo"**.
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
# depois é só procurar "M Finance" no menu de aplicativos, ou rodar:
mfinance
```

---

## 🚀 Primeiro uso

1. Na primeira vez, o app abre um **assistente de configuração** que te guia passo a passo.
2. Você vai precisar de uma **chave de API da Pierre** — gere em <https://pierre.finance/api-key>.
3. Cole a chave, conecte suas contas e clique em **"Iniciar sincronização"**. O app baixa contas, transações e faturas para o banco local.
4. Pronto: painel, planejamento, alertas e assistente já ficam disponíveis.

A partir daí tudo funciona offline — novas sincronizações só acontecem quando você pede.

---

## 💾 Onde ficam os seus dados

O banco de dados local e a chave de criptografia ficam separados por usuário:

| Sistema | Pasta |
| --- | --- |
| Windows | `%APPDATA%\openfinance-desktop\` |
| Linux | `~/.config/openfinance-desktop/` |

Para **fazer backup**, copie o `openfinance.db` (e o `.master-key`) dessa pasta. Para **começar do zero**, feche o app e apague essa pasta.

---

## ❓ Problemas comuns

- **SmartScreen no Windows / "app não verificado":** esperado, porque o instalador não é assinado. Veja o passo 3 da seção do Windows.
- **App não abre no Linux:** rode pelo terminal com `--no-sandbox` para ver as mensagens de erro.
- **Erro de sincronização logo de cara:** feche o app e abra de novo — a maioria dos problemas de banco se corrige sozinha na inicialização. Se persistir num banco muito antigo, apague a pasta de dados acima para recomeçar limpo.

---

## 🔒 Privacidade

Os seus dados financeiros ficam no **seu** computador, num banco SQLite com os segredos criptografados (AES-256-GCM). Nada é enviado para servidores de terceiros além das chamadas que **você** autoriza à API da Pierre durante a sincronização.

---

_M Finance v0.1.0_
