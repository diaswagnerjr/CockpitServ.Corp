# CockpitServ.Corp

Cockpit de gestão da área de Serviços Corporativos da Suzano, criado para centralizar processos, agendas, calendário de sourcing, toolkit de contratação e monitoramento de pontos críticos, apoiando o planejamento e a gestão semanal do time.

## Status do MVP

- Site estático em `index.html`, pronto para GitHub Pages.
- Leitura pública via Supabase Data API.
- Edição apenas para admin autenticado.
- Admin inicial liberado: `wagnerdj@suzano.com.br`.
- Backend aplicado no projeto Supabase `wagner-performance-os` (`reebavnvftfibyhhjxat`).

## Módulos

- Processos & Rotinas: modelo operacional com processo esperado, gaps e proposta To Be.
- Tool Kit e Radar: checklist não exaustivo para Etapa 01, Etapa 02 e processos com ativos, com download CSV.
- Processos críticos: matriz criticidade x urgência e conclusão de críticos por admin.
- Visão geral de sourcing: pipeline ahead 2026/2027 por mês, pilar e spend.
- Calendário de gates: agenda baseada na planilha Resumo Gates.

## Supabase

Para preservar o outro front do projeto, os dados foram criados em schemas novos:

- `cockpit_servcorp`: tabelas do cockpit.
- `cockpit_private`: função de autorização admin.

Como a Data API expõe `public` por padrão, o app usa views públicas prefixadas `csc_*` com `security_invoker = true`. Os dados continuam armazenados no schema isolado e o RLS decide quem lê/escreve.

Tabelas carregadas inicialmente:

- `critical_processes`: 3 registros.
- `sourcing_processes`: 9 registros.
- `gate_events`: 7 registros.
- `inspiration_files`: 3 registros.
- `admin_users`: 1 registro.

## Admin

Não há cadastro público no site. Para liberar novos editores:

1. Crie o usuário no Supabase Auth.
2. Insira o e-mail em `cockpit_servcorp.admin_users`.

O time pode visualizar tudo sem login. Escrita anônima foi bloqueada por RLS/grants.
