# Teddy Open Finance App

Aplicação React simples que exibe "Hello Teddy Open Finance".

## Requisitos

- Node.js (versão 14 ou superior)
- npm ou yarn

## Instalação

```bash
npm install
```

## Desenvolvimento

Para iniciar o servidor de desenvolvimento:

```bash
npm start
```

A aplicação estará disponível em [http://localhost:3000](http://localhost:3000).

## Build

Para criar a versão de produção:

```bash
npm run build
```

Os arquivos estáticos serão gerados na pasta `build/`.

## Deploy

O deploy é automatizado via GitHub Actions usando **OIDC com IAM Roles** (sem necessidade de chaves de acesso). Ao fazer push para a branch `main`, o workflow irá:

1. Fazer o build da aplicação
2. Fazer upload dos arquivos para o bucket S3
3. Invalidar o cache do CloudFront

### Configuração do Deploy

#### Pré-requisitos AWS

Antes de configurar o GitHub Actions, você precisa:

1. **Criar OIDC Identity Provider no IAM** (consulte [AWS_SETUP.md](./AWS_SETUP.md))
2. **Criar IAM Role** com permissões para S3 e CloudFront
3. **Criar bucket S3** para hospedar os arquivos estáticos
4. **Criar distribuição CloudFront** apontando para o bucket S3

#### Secrets do GitHub

Configure o seguinte **Secret** no repositório:

**Caminho:** Settings → Secrets and variables → Actions → Secrets

| Nome | Descrição | Exemplo |
|------|-----------|---------|
| `AWS_ROLE_ARN` | ARN da IAM Role criada para o GitHub Actions | `arn:aws:iam::accountid:role/GitHubActionsDeployRole` |

#### Variables do GitHub

Configure as seguintes **Variables** no repositório:

**Caminho:** Settings → Secrets and variables → Actions → Variables

| Nome | Descrição | Exemplo |
|------|-----------|---------|
| `AWS_REGION` | Região AWS onde o bucket S3 está localizado | `us-east-1` |
| `S3_BUCKET` | Nome do bucket S3 para hospedar os arquivos | `teddy-app` |
| `CLOUDFRONT_DISTRIBUTION_ID` | ID da distribuição CloudFront | `XXXXXXXXXXXXXXX` |

#### Variáveis de Ambiente Locais

Este projeto não requer variáveis de ambiente para desenvolvimento local. Todas as configurações são específicas para o deploy via GitHub Actions.

## Tecnologias

- React 18
- GitHub Actions
- AWS S3
- AWS CloudFront
