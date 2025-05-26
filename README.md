# Sistema de Controle de Atestados - Estrutura Completa para VSCode

Este repositório contém a estrutura completa do Sistema de Controle de Atestados, desenvolvido como uma aplicação PWA (Progressive Web App) com backend em Flask e frontend em React, pronta para uso no Visual Studio Code em ambiente Windows.

## Visão Geral

O sistema foi projetado para gerenciar o fluxo de atestados médicos entre os seguintes agentes:

1. **Servidor**: Submete atestados e acompanha seu status
2. **Recepção**: Verifica a conformidade dos atestados com a Resolução CFM nº 2381/2024
3. **Medicina Ocupacional**: Analisa tecnicamente os atestados e toma decisões
4. **Enfermagem**: Comunica resultados aos servidores

## Estrutura do Projeto

```
atestados_pwa_vscode/
├── backend/                # API e servidor em Flask
│   ├── src/                # Código-fonte principal
│   │   ├── models/         # Modelos de dados
│   │   ├── routes/         # Rotas da API
│   │   ├── static/         # Arquivos estáticos
│   │   ├── templates/      # Templates HTML
│   │   └── utils/          # Utilitários e helpers
│   ├── tests/              # Testes automatizados
│   ├── docs/               # Documentação
│   ├── app.py              # Ponto de entrada da aplicação
│   ├── config.py           # Configurações da aplicação
│   └── requirements.txt    # Dependências do projeto
│
└── frontend/               # Aplicação React PWA
    ├── public/             # Arquivos públicos
    ├── src/                # Código-fonte principal
    │   ├── assets/         # Imagens, ícones e outros recursos
    │   ├── components/     # Componentes reutilizáveis
    │   ├── contexts/       # Contextos React (estado global)
    │   ├── hooks/          # Hooks personalizados
    │   ├── pages/          # Páginas da aplicação
    │   ├── services/       # Serviços de API e utilitários
    │   ├── styles/         # Estilos CSS/Tailwind
    │   └── utils/          # Funções utilitárias
    └── package.json        # Dependências e scripts
```

## Configuração do Ambiente de Desenvolvimento

### Pré-requisitos

- Visual Studio Code
- Python 3.9+
- Node.js 16+
- MySQL 8.0+ (ou outro banco de dados compatível)

### Configuração do Backend

1. Abra o diretório `backend` no VSCode
2. Crie um ambiente virtual Python:
   ```bash
   # No terminal do VSCode (Windows)
   python -m venv venv
   venv\Scripts\activate
   ```
3. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```
4. Configure as variáveis de ambiente:
   ```bash
   # Copie o arquivo .env.example para .env
   copy .env.example .env
   # Edite o arquivo .env com suas configurações
   ```
5. Inicialize o banco de dados:
   ```bash
   python app.py init-db
   ```
6. Execute o servidor:
   ```bash
   python app.py
   ```

### Configuração do Frontend

1. Abra o diretório `frontend` no VSCode
2. Instale as dependências:
   ```bash
   npm install
   # ou
   yarn install
   ```
3. Execute o aplicativo:
   ```bash
   npm start
   # ou
   yarn start
   ```

## Fluxo do Sistema

1. **Submissão do Atestado** (Servidor)
   - Upload do atestado (imagem ou PDF)
   - Preenchimento de informações complementares
   - Status inicial: "Aguardando Verificação"

2. **Verificação de Conformidade** (Recepção)
   - Checklist de requisitos conforme a Resolução CFM
   - Aprovação ou rejeição do atestado
   - Status após aprovação: "Verificado"
   - Status após rejeição: "Não Conforme"

3. **Análise Técnica** (Medicina Ocupacional)
   - Análise do histórico médico e do atestado
   - Decisão: Deferimento total, parcial ou indeferimento
   - Status após análise: "Deferido Total", "Deferido Parcial" ou "Indeferido"

4. **Comunicação de Resultado** (Enfermagem)
   - Comunicação ao servidor em caso de deferimento parcial ou indeferimento
   - Registro do contato realizado
   - Status após comunicação: "Comunicado"
   - Status final: "Concluído"

## Recursos Implementados

- **Autenticação**: Sistema de login e controle de acesso por perfil
- **Upload de Arquivos**: Suporte para upload de atestados em diversos formatos
- **Validação de Dados**: Verificação de conformidade com requisitos legais
- **Fluxo de Trabalho**: Transições de status e notificações
- **Interface Responsiva**: Adaptada para desktop e dispositivos móveis
- **PWA**: Suporte para instalação como aplicativo

## Próximos Passos

1. Implementar testes unitários e de integração
2. Configurar CI/CD para implantação automática
3. Adicionar recursos de relatórios e estatísticas
4. Implementar notificações em tempo real

## Notas Importantes

- Esta estrutura resolve o problema de importação cruzada entre modelos SQLAlchemy, utilizando o padrão recomendado de definir relacionamentos após a declaração de todas as classes
- O frontend está configurado como PWA, permitindo instalação em dispositivos móveis
- A estrutura é compatível com desenvolvimento em Windows, Linux e macOS
