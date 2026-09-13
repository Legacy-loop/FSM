Aqui está a documentação completa em **Markdown (`README.md`)** explicando o funcionamento do mini projeto, ideal para inclusão no repositório.

---

# 🥤 Máquina de Vendas Interativa — FSM (Finite State Machine)

Este projeto é uma simulação interativa de uma **Máquina de Vendas de Bebidas** baseada no conceito de **Máquina de Estados Finitos (FSM)**. O objetivo principal é demonstrar de forma visual, clara e reativa como a teoria de automatos e estados finitos se aplica no funcionamento de sistemas do mundo real.

---

## 🛠️ Tecnologias Utilizadas

* **HTML5**: Estruturação da página e acessibilidade.
* **CSS3 / Flexbox & Grid**: Layout responsivo, componentes estilizados em tema escuro industrial (*dashboard style*), efeitos de *glassmorphism* e animações CSS.
* **SVG (Scalable Vector Graphics)**: Renderização gráfica e vetorial do diagrama de estados, transições e rótulos.
* **JavaScript (ES6+)**: Implementação pura da lógica da máquina de estados finitos e atualização em tempo real dos elementos DOM/SVG.

---

## 💡 Como Funciona o Sistema

### 1. Regra de Negócio

* **Preço Fixo da Bebida:** `30¢` (30 centavos).
* **Moedas Aceitas:** `5¢`, `10¢` e `25¢`.
* **Saldo Inicial:** `0¢`.
* **Mecanismo de Troco:** Quando o saldo atinge um valor igual ou superior a `30¢`, o produto é liberado, o troco é calculado como `(Saldo Final - 30¢)` e o sistema retorna automaticamente ao estado inicial (`saldo 0`) após 3,6 segundos.

---

## 🔄 A Máquina de Estados Finitos (FSM)

A FSM é composta por **estados** (representados pelos nós circulares) e **transições** (as setas rotuladas com o valor da moeda inserida).

### 📍 Tipos de Estados

1. **Estado Inicial:**
* **`saldo 0`**: Ponto de partida de qualquer transação.


2. **Estados Intermediários:**
* **`saldo 5`**, **`saldo 10`**, **`saldo 15`**, **`saldo 20`**, **`saldo 25`**: Acumulam o valor inserido aguardando o atingimento do preço mínimo de `30¢`.


3. **Estados Finais (Aceitação):**
* **`saldo 30`** (Troco: `0¢`)
* **`saldo 35`** (Troco: `5¢`)
* **`saldo 40`** (Troco: `10¢`)
* **`saldo 45`** (Troco: `15¢`)
* **`saldo 50`** (Troco: `20¢`)



---

## 🔀 Tabela de Transições

A lógica JavaScript utiliza uma tabela de mapeamento estrito para transitar entre estados com base na moeda inserida:

| Estado Atual | Moeda `5¢` | Moeda `10¢` | Moeda `25¢` |
| --- | --- | --- | --- |
| **`0`** | `5` | `10` | `25` |
| **`5`** | `10` | `15` | `30` *(Final)* |
| **`10`** | `15` | `20` | `35` *(Final)* |
| **`15`** | `20` | `25` | `40` *(Final)* |
| **`20`** | `25` | `30` *(Final)* | `45` *(Final)* |
| **`25`** | `30` *(Final)* | `35` *(Final)* | `50` *(Final)* |

> **Nota de Validação:** Transições não mapeadas (ex: inserir `10¢` estando no `saldo 20`) resultam na rejeição da moeda pela máquina, mantendo o estado atual intacto.

---

## 🗺️ Organização do Diagrama SVG

O diagrama vetorial foi estruturado em **4 colunas bem definidas** para garantir leitura limpa e sem cruzamento de linhas:

```text
[ Coluna 1 ]     [ Coluna 2 ]     [ Coluna 3 ]       [ Coluna 4 (Finais) ]
  saldo 0  --->    saldo 5   --->   saldo 15   --->     saldo 30 (Troco 0)
                   saldo 10  --->   saldo 20   --->     saldo 35 (Troco 5)
                                    saldo 25   --->     saldo 40 (Troco 10)
                                                        saldo 45 (Troco 15)
                                                        saldo 50 (Troco 20)

```

* **Setas & Conexões:** Utilizam curvas Bézier (`path`) com marcadores SVG para indicar o fluxo.
* **Destaque Visual do Estado Atual:** O estado em que a máquina se encontra recebe uma classe CSS `.current` que ativa um contorno animado verde *glowing* (`#22C55E`).
* **Estados Finais:** Possuem anéis duplos com destaque amarelado/dourado (`#FACC15`).

---

## 🚀 Como Executar o Projeto

1. Baixe ou clone o repositório.
2. Abra o arquivo `index.html` (ou o nome atribuído ao arquivo HTML) em qualquer navegador moderno.
3. Nenhuma instalação ou dependência externa de build (Node.js, Webpack, etc.) é necessária.

---

## 🕹️ Como Interagir

1. Clique nos botões de moeda (**5¢**, **10¢**, **25¢**) no painel lateral.
2. Observe o **Visor de Saldo** e o **Diagrama SVG** mudarem em tempo real, destacando o nó verde ativo.
3. Ao atingir `30¢` ou mais:
* O visor mostrará **`PRODUTO DISPENSADO`**.
* O troco correspondente será exibido no painel inferior.
* Os botões serão desabilitados temporariamente por 3.6s antes de reiniciar a máquina para `saldo 0`.


4. Use o botão **↻ Reiniciar máquina** a qualquer momento para forçar o reset ao estado inicial.
