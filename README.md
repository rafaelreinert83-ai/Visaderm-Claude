# Visaderm-Claude# Visaderm Day Hospital — Sistema Clínico v16.4

<div align="center">

**VISADERM DAY HOSPITAL**  
*Dr. Rafael Reinert · CRM/SC 16789*  
Dermatologia & Transplante Capilar · Blumenau — SC

[![Deploy](https://img.shields.io/badge/Vercel-Deploy-black?logo=vercel)](https://visaderm-claude-qrq4.vercel.app)
[![License](https://img.shields.io/badge/License-Privado-red)](#)
[![HTML](https://img.shields.io/badge/Stack-HTML%20%2F%20CSS%20%2F%20JS-orange)](#)
[![AI](https://img.shields.io/badge/AI-Claude%20Sonnet%204-blueviolet)](https://anthropic.com)
[![LGPD](https://img.shields.io/badge/LGPD-Conforme-green)](#)

</div>

-----

## Sobre o Sistema

Prontuário digital clínico desenvolvido exclusivamente para a **Visaderm Day Hospital**, especializada em transplante capilar FUE e dermatologia. Sistema single-file HTML com inteligência artificial integrada via API Anthropic (Claude Sonnet 4), projetado para uso no iPhone em ambiente cirúrgico.

> *“Cada unidade folicular é singular e irrepetível. Transplantá-la com precisão é ciência. Devolvê-la com naturalidade é arte.”*  
> — Dr. Rafael Reinert

-----

## Funcionalidades

### Módulos Principais

|Módulo                |Descrição                                                      |
|----------------------|---------------------------------------------------------------|
|**Dashboard**         |Estatísticas em tempo real, agenda do dia, alertas clínicos    |
|**Pacientes**         |Cadastro com validação CPF (dígito verificador), LGPD, busca   |
|**Prontuário Digital**|IA diagnóstica Norwood/Ludwig/Sinclair, Doppler, Hairmetrix    |
|**Procedimentos**     |Mapa anestésico intraoperatório, contagem de UFs, protokolo FUE|
|**GraftScan AI™**     |Análise folicular em tempo real com VQS™ e GII™ via Claude     |
|**Scalpscan AI**      |Mapeamento da zona receptora com inteligência artificial       |
|**Pós-Op**            |Timeline evolutiva 12 meses, comparador fotográfico com slider |
|**Exames**            |Hairmetrix (PDF/imagem/manual), Doppler com alerta RI ≥ 0.71   |

### Módulos Avançados (v16.4)

|Módulo                     |Descrição                                                       |
|---------------------------|----------------------------------------------------------------|
|**Mapa SVG Couro Cabeludo**|8 zonas interativas, planejamento de densidade e UFs            |
|**Exame BHT**              |Body Hair Transplant — 7 zonas corporais, score de viabilidade  |
|**Farmácia + Barcode**     |Scanner BarcodeDetector API, etiquetas CODE-128, rastreio ANVISA|
|**NFS-e ABRASF 2.04**      |Emissão de nota fiscal eletrônica, XML, cálculo ISS Blumenau-SC |
|**Portal do Paciente**     |QR Code, timeline pós-op, orientações, envio automático WhatsApp|
|**Laboratórios FHIR R4**   |Receptor de resultados HL7 FHIR R4, alertas de valores críticos |
|**GraftScan Anotação**     |Canvas com 6 ferramentas de anotação, export PNG com watermark  |

-----

## Stack Técnica

```
Frontend:   HTML5 + CSS3 + JavaScript ES2020 (single-file, sem framework)
IA:         Anthropic Claude claude-sonnet-4-20250514 via API
Validação:  Zod 3.22.4 (client-side, defer) + Regex clínico brasileiro
Auth:       Login simples + session storage
Storage:    localStorage (vsd_v16) + IndexedDB (imagens GraftScan)
Crypto:     SubtleCrypto SHA-256 (HTTPS) / fallback simpleHash (HTTP)
Deploy:     GitHub → Vercel (auto-deploy por push)
CDNs:       Chart.js 4.4, Font Awesome 6.5, JsBarcode 3.11 (lazy)
```

-----

## Segurança e Conformidade

- **LGPD (Lei 13.709/2018)** — consentimento registrado no cadastro
- **CFM Resolução 1.821/07** — prontuário com integridade e rastreabilidade
- **CFM Resolução 2.299/21** — registro de procedimentos cirúrgicos
- **Validação Zod** — schemas para paciente, NFS-e, medicamentos, FHIR
- **Sanitização XSS** — todos os inputs validados antes de render
- **CPF com dígito verificador** — algoritmo completo client-side
- **Rate limiting** — middleware Vercel Edge (API Claude: 20 req/min)
- **CSP Headers** — Content Security Policy em todas as respostas

-----

## Dados Clínicos

|Parâmetro                   |Referência                 |
|----------------------------|---------------------------|
|Escala Norwood-Hamilton     |I a VII                    |
|Escala Ludwig / Sinclair    |I a III                    |
|Alerta Doppler temporal     |RI ≥ 0.71                  |
|Lidocaína sem vasoconstritor|4.5 mg/kg                  |
|Lidocaína com epinefrina    |7.0 mg/kg                  |
|Protocolo GraftScan         |15 cm da mesa, aumento 2.5x|
|Punch Trivellini            |0.75 — 1.00 mm             |

-----

## Credenciais de Acesso

```
Login:  Visaderm
Senha:  1234
```

> Para uso clínico real: configure autenticação via Supabase Auth

-----

## Deploy

O sistema é hospedado no Vercel com deploy automático a partir deste repositório.

```
URL: https://visaderm-claude-qrq4.vercel.app
Branch de produção: Roots
```

Para atualizar: faça push para a branch `Roots` ou configure `Main` como branch de produção nas Settings do Vercel.

-----

## Arquitetura de API (próximo passo)

```
/
├── index.html              # Sistema completo (296KB)
├── middleware.js           # Vercel Edge — rate limit, WAF, CORS, CSP
├── vercel.json             # Configuração de rotas e env vars
└── api/
    ├── _middleware.js      # Zod schemas + withValidation + withAuth
    ├── claude-proxy.js     # Proxy Anthropic — chave nunca no browser
    ├── patients.js         # CRUD pacientes com validação
    ├── nfse.js             # Emissão NFS-e ABRASF 2.04
    ├── pharmacy.js         # Controle de estoque farmacêutico
    └── health.js           # Health check público
```

-----

## Roadmap

- [ ] Migração para Supabase (PostgreSQL + Auth + Storage) — região São Paulo
- [ ] Backend real via Vercel Edge Functions (substituir localStorage)
- [ ] Assinatura digital ICP-Brasil (RSA-PSS 2048-bit + TSA Certisign)
- [ ] Integração webservice NFS-e Prefeitura de Blumenau (ISS.net)
- [ ] Integração FHIR R4 com Fleury e DASA
- [ ] App React Native (iOS) via Expo
- [ ] Relatórios PDF clínicos automatizados

-----

## Desenvolvido com

- [Anthropic Claude](https://anthropic.com) — IA clínica e geração de código
- [Vercel](https://vercel.com) — deploy e edge functions
- [Chart.js](https://chartjs.org) — gráficos financeiros e evolutivos
- [Font Awesome](https://fontawesome.com) — ícones
- [Zod](https://zod.dev) — validação de schemas

-----

<div align="center">

**Visaderm Day Hospital**  
Blumenau — Santa Catarina — Brasil  
`@visaderm` · `@dr.rafaelreinert`

*Sistema desenvolvido para uso clínico exclusivo. Dados de pacientes protegidos por LGPD.*

</div>
