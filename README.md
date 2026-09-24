# NewRH

Sistema de RH full stack para gestão do processo seletivo e de admissão de colaboradores: portal público de vagas e candidaturas, painel interno para gestores/RH, aprovação de abertura de vagas, banco de talentos, programa de menor aprendiz, pasta digital do colaborador (integrada ao SharePoint) e notificações automáticas por e-mail.

> Este projeto é uma versão genérica/sanitizada, sem dados ou identidade de nenhuma empresa real. Todos os e-mails, nomes e domínios de exemplo usam `empresaexemplo.com.br`.

## Stack

- **Backend:** Python (Flask), SQLAlchemy, PostgreSQL (via `pg8000`), JWT, bcrypt
- **Frontend:** HTML, CSS e JavaScript puro (sem framework)
- **Integrações:** Microsoft Graph API / OAuth2 (login SSO e SharePoint), envio de e-mail via Microsoft Graph
- **Deploy:** Gunicorn + gevent

## Funcionalidades

- Portal público de vagas com candidatura online e acompanhamento por CPF
- Login corporativo via Microsoft SSO com controle de acesso por papel (Admin, Owner, Viewer, Gestor)
- Fluxo de solicitação e aprovação de abertura de vagas
- Painel de gestão de candidaturas e processos seletivos, com etapas configuráveis
- Banco de talentos e programa de menor aprendiz
- Pasta digital do colaborador com estrutura de pastas automatizada no SharePoint
- Alertas automáticos (candidatos parados em uma etapa) e notificações por e-mail
- Auditoria de ações (log de eventos)

## Configuração

1. Instale as dependências do backend:
   ```bash
   cd backend
   pip install -r requirements.txt
   ```
2. Copie `backend/.env.example` para `backend/.env` e preencha com seus próprios valores (banco de dados, chave secreta, credenciais do Azure AD/Microsoft Graph, etc.).
3. Rode o servidor:
   ```bash
   python main.py
   ```
   O frontend estático é servido automaticamente pelo próprio Flask.

## Estrutura do projeto

```
backend/    → API Flask, modelos, rotas e integrações
frontend/   → páginas HTML/CSS/JS do portal e do painel interno
migration_solicitacoes.sql → script de migração do banco de dados
```

## Variáveis de ambiente

Veja `backend/.env.example` para a lista completa. As principais são:

| Variável | Descrição |
|---|---|
| `DATABASE_URL` | String de conexão do PostgreSQL |
| `SECRET_KEY` | Chave usada para assinar os tokens JWT |
| `MS_TENANT_ID` / `MS_CLIENT_ID` / `MS_CLIENT_SECRET` | Credenciais do app registrado no Azure AD (login SSO, e-mail, SharePoint) |
| `BASE_URL` | URL pública onde a aplicação está hospedada |
| `SHAREPOINT_COLAB_FILE_ID` | ID do arquivo Excel de colaboradores no SharePoint |

## Licença

Projeto pessoal para fins de portfólio.
