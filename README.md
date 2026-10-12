# Testes de Performance da API do Banco com K6

Repositório com testes de performance automatizados desenvolvidos com a ferramenta [Grafana k6](https://k6.io/) e escritos em JavaScript, voltados para a API do sistema bancário.

🔗 Repositório: [github.com/juliodelimas/banco-api-performance](https://github.com/juliodelimas/banco-api-performance)

---

## 📌 Introdução

Este projeto tem como objetivo simular diferentes cargas e cenários de uso para a API do banco, avaliando seu desempenho e identificando possíveis gargalos. Os testes são escritos com foco em modularidade, organização por contexto e reutilização de modelos de dados.

---

## ⚙️ Tecnologias Utilizadas

- [k6](https://k6.io/) – Ferramenta open source de testes de carga e performance.
- JavaScript (ES6)
- [GJSON](https://github.com/tidwall/gjson) – Para extração de dados em respostas JSON.
- Variáveis de ambiente para configuração dinâmica (ex.: `BASE_URL`).

---

## 📁 Estrutura do Repositório

```text
banco-api-performance/
├── fixtures/             # Dados de entrada para os testes (usuários, payloads etc.)
├── helpers/              # Funções utilitárias reutilizáveis para interação com a API
├── tests/                # Casos de teste organizados por módulo da API
├── utils/                # Outras funções utilitárias reutilizáveis
├── config/               # Arquivos de configuração
└── README.md             # Este documento
```

---

## 🗂️ Objetivo de Cada Grupo de Arquivos

- **`fixtures/`**: dados de entrada para os testes, como usuários e payloads.
- **`helpers/`**: funções reutilizáveis para operações comuns de interação com a API.
- **`tests/`**: casos de teste organizados por módulo da API.
- **`utils/`**: outras funções utilitárias compartilhadas.
- **`config/`**: arquivos de configuração utilizados pelo projeto.

---

## 💻 Instalação e Execução

### 1. Clone o repositório

```bash
git clone https://github.com/juliodelimas/banco-api-performance.git
cd banco-api-performance
```

### 2. Configure as variáveis de ambiente

Se o projeto utilizar o arquivo `config.local.json`, configure nele a URL base da API que será testada. Exemplo:

```json
{
  "baseUrl": "http://localhost:3000"
}
```

> **Observação:** o k6 não carrega automaticamente um arquivo JSON de configuração arbitrário. O projeto precisa ter código que leia esse arquivo, ou a URL deve ser fornecida por variável de ambiente.

### 3. Execute um teste

Exemplo de execução de um teste de login:

```bash
k6 run tests/login.test.js
```

Caso o script leia a URL base da variável de ambiente `BASE_URL`, execute:

```bash
k6 run tests/autenticacao/login.test.js -e BASE_URL=http://localhost:3000
```

> Ajuste o caminho do arquivo de teste conforme a estrutura real do repositório.

### 4. Acompanhe a execução e exporte um relatório HTML

É possível habilitar o dashboard web do k6 e exportar um relatório HTML ao final da execução. Em shells compatíveis com a sintaxe abaixo:

```bash
K6_WEB_DASHBOARD=true \
K6_WEB_DASHBOARD_EXPORT=html-report.html \
k6 run tests/autenticacao/login.test.js \
-e BASE_URL=http://localhost:3000
```

Ao finalizar a execução, o arquivo `html-report.html` deverá ser gerado no diretório de execução, desde que a versão do k6 instalada ofereça suporte a essas opções.

---

## 📊 Análise dos resultados

Ao analisar a execução, observe as métricas relevantes para o cenário e os critérios definidos para o teste, por exemplo:

- Duração das requisições e percentis de tempo de resposta.
- Taxa de requisições com falha.
- Resultados dos checks.
- Thresholds configurados e indicação de aprovação ou falha.
- Quantidade de usuários virtuais e duração da carga aplicada.

Os limites de aprovação devem ser definidos conforme os requisitos de performance da API e o objetivo de cada teste.

---

## 📝 Observações

- Confirme que a API está em execução e acessível antes de iniciar os testes.
- Utilize uma URL correspondente ao ambiente correto.
- Não versione credenciais, tokens ou outros dados sensíveis.
- Confirme os caminhos dos scripts e os arquivos de configuração existentes no repositório antes de executar os comandos.
