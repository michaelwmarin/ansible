# Ansible: Implantação Automatizada de WordPress com MySQL

![Ansible](https://img.shields.io/badge/Ansible-2.9%2B-blue.svg)
![WordPress](https://img.shields.io/badge/Service-WordPress-blue)
![MySQL](https://img.shields.io/badge/Database-MySQL-orange)
![License](https://img.shields.io/badge/License-MIT-green.svg)

Este projeto é o resultado prático do curso de **Ansible da Alura**, aplicando as melhores práticas de automação para implantar um ambiente WordPress de forma eficiente e escalável em múltiplas máquinas virtuais.

O playbook `provisioning.yml` automatiza todo o processo, desde a configuração da infraestrutura até a instalação final do WordPress, separando a aplicação e o banco de dados em servidores distintos.

---

## 🎓 A Jornada do Projeto

Este repositório documenta a evolução de um processo de automação, desde os primeiros passos até uma arquitetura modular e reutilizável.

1.  **Criação do Ambiente**: No início, o projeto começou com a configuração de máquinas virtuais e a definição de chaves de acesso SSH para garantir a comunicação segura com o Ansible.

2.  **Primeiro Playbook**: O playbook inicial, `provisioning.yml`, foi criado para centralizar as tarefas. Com o avanço do projeto, ele se tornou mais enxuto e declarativo.

3.  **Modularização com Roles**: Para organizar o código e facilitar o reuso, o playbook foi dividido em **roles**, onde cada uma executa uma tarefa específica:
    -   A **role do WordPress** cuida da criação de diretórios, download, descompressão de arquivos e configuração do Apache.
    -   A **role do MySQL** gerencia a criação de tabelas, usuários e a liberação de acesso remoto ao banco de dados.

4.  **Uso de Handlers**: Foram implementados *handlers* para reiniciar serviços (como Apache e MySQL) de forma otimizada, ou seja, apenas quando um arquivo de configuração era de fato alterado.

5.  **Gerenciamento de Dependências**: Para garantir a ordem correta de execução, foi definida uma dependência explícita, onde a `role` do WordPress só é executada após a conclusão bem-sucedida da `role` do MySQL.

6.  **Arquitetura Distribuída**: O ambiente final foi dividido em duas máquinas virtuais: uma dedicada a gerenciar o WordPress e o Apache, e outra exclusiva para o banco de dados MySQL, simulando um ambiente de produção mais realista.

---

## ✨ Funcionalidades

-   **Provisionamento Completo**: Automatiza a configuração de um ambiente web do zero.
-   **Separação de Serviços**: Isola o servidor de aplicação (WordPress/Apache) do servidor de banco de dados (MySQL).
-   **Configuração Dinâmica**: Utiliza templates para gerar arquivos de configuração, como o `wp-config.php`.
-   **Gerenciamento Inteligente de Serviços**: Reinicia serviços apenas quando necessário, graças ao uso de handlers.
-   **Código Limpo e Reutilizável**: A estrutura baseada em roles permite que cada componente seja facilmente mantido ou utilizado em outros projetos.

---

## ⚙️ Como Executar

### 1. Pré-requisitos
-   Ansible instalado na máquina de controle.
-   Acesso SSH com chave pública para os servidores de destino.

### 2. Configuração
-   Clone este repositório.
-   Edite o arquivo de inventário (`hosts`) com os IPs das suas máquinas virtuais.
-   Ajuste as credenciais e configurações nos arquivos de `group_vars`. (Recomenda-se o uso do **Ansible Vault** para proteger dados sensíveis).

### 3. Execução
Execute o playbook principal para provisionar todo o ambiente:
```bash
ansible-playbook provisioning.yml
