# Deploy da landing page PainelLog

Site estático (um `index.html` com tudo embutido). Hospedagem: **GitHub Pages**,
domínio final **painellogapp.com.br**.

## Pré-requisito

Registrar **painellogapp.com.br** no Registro.br (mesma conta do nobredias).

## Passo 1 — Ativar o GitHub Pages

1. GitHub → repositório **PainelLogLandingPage** → aba **Settings**
2. Menu lateral **Pages**
3. Em **Build and deployment** → Source: **Deploy from a branch**
4. Branch: **main** / pasta **/ (root)** → **Save**
5. O arquivo `CNAME` do repo já define o domínio `painellogapp.com.br` automaticamente.
   Enquanto o DNS (passo 2) não estiver pronto, o GitHub mostra um aviso de
   "DNS check" — é esperado.

Link temporário (só funciona se o CNAME for removido): `https://rodrigovicentedev.github.io/PainelLogLandingPage/`

## Passo 2 — DNS no Registro.br

No painel do domínio (Editar Zona / DNS), criar:

**Apex (painellogapp.com.br) → 4 registros A:**

```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```

**IPv6 (opcional, recomendado) → 4 registros AAAA:**

```
AAAA   @   2606:50c0:8000::153
AAAA   @   2606:50c0:8001::153
AAAA   @   2606:50c0:8002::153
AAAA   @   2606:50c0:8003::153
```

**www → CNAME:**

```
CNAME   www   rodrigovicentedev.github.io.
```

> IPs oficiais do GitHub Pages (conferir em docs.github.com se houver dúvida:
> "Managing a custom domain for your GitHub Pages site").

## Passo 3 — HTTPS

Depois que o DNS propagar (de minutos a algumas horas):

1. Settings → Pages → confirmar que **Custom domain** = `painellogapp.com.br` (verde, verificado)
2. Marcar **Enforce HTTPS** (o certificado Let's Encrypt é emitido automaticamente;
   a opção pode levar alguns minutos para ficar disponível)

## Passo 4 — Testes finais

- [ ] Abrir `https://painellogapp.com.br` e `https://www.painellogapp.com.br`
- [ ] Conferir o logo, o FAQ e o layout no celular
- [ ] **Enviar o formulário de verdade** e confirmar que o lead chega no e-mail
      vinculado à chave do Web3Forms (a chave define o e-mail de destino, não o código)

## Atualizar o site depois

Qualquer mudança no `index.html`:

```bash
git add -A
git commit -m "..."
git push origin main
```

O GitHub Pages republica sozinho em ~1 minuto.

## Observações

- O domínio do **produto/aplicação** (`app.painellogapp.com.br`, `*.painellogapp.com.br`)
  é outra configuração, feita quando a Aplicação for para produção. Esta landing usa
  só o apex + www.
- A chave do Web3Forms está no `index.html` (campo `access_key`). É uma chave pública
  de formulário (pode ficar no código); o controle anti-spam é o honeypot + o painel do Web3Forms.
