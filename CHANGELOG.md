# Histórico de Versões — MilaTec Sistema

## v3.58 — 2026-07-03
### Corrigido
- Drawer de atividade agora sempre abre na aba **Geral** (antes podia ficar preso em Subtarefas/Colaboração, ocultando os campos de Tipo e Área)
- Mecanismo de auto-reload por versão para garantir que todos os usuários carreguem o código mais recente automaticamente

---

## v3.57 — 2026-07-03
### Corrigido
- Saudação restaurada com horário de Brasília: **Bom dia / Boa tarde / Boa noite** (havia sido sobrescrita para "Olá" ao carregar o perfil do usuário)
- Auto-reload forçado por versão (`_sys_version` no localStorage) para invalidar cache do navegador em todos os usuários

---

## v3.56 — 2026-07-03
### Corrigido
- **Campo Tipo de atividade**: opções do select alinhadas com os valores reais do banco (Projeto Executivo, Proposta Comercial, Pré-projeto, ART, Cálculo Estrutural, Dossiê Técnico, Projeto para Aprovação)
- **Campo Área**: adicionada opção "Compras"; corrigido "Processos " com espaço extra no banco de dados

---

## v3.55 — 2026-07-03
### Corrigido
- Erro `invalid input syntax for type uuid: "null"` ao salvar alterações de atividade: adicionada validação UUID antes do `.update().eq('id', _taskEditId)` no caminho `idx === -1`

---

## v3.54 — 2026-07-02
### Corrigido
- Erro `invalid input syntax for type uuid: "null"` em `_syncAtividadeVinculos`: adicionada função `safeUuid()` que descarta valores inválidos (string "null", undefined) antes de inserir nas junction tables

---

## v3.53 — 2026-07-02
### Adicionado
- Salvar alterações de atividades do Supabase: ao editar uma atividade que já existe no banco (não apenas no localStorage), as mudanças agora são persistidas via UPDATE no Supabase

---

## v3.52 — 2026-07-02
### Corrigido
- Fotos de perfil (avatars) dos usuários aparecem no painel admin
- Nomes exibidos no admin agora usam `nome_display` do perfil (prioridade sobre metadado do convite)
- Link de redefinição de senha e convite de primeiro acesso agora apontam para a URL de produção (`https://lorenacodes.github.io/milatec-sistema`) em vez de `localhost:3000`

---

## v3.51 e anteriores — Migração do banco de dados
### Migrado
- Migração completa do Airtable para Supabase (PostgreSQL)
- Tabelas migradas: `obras`, `projetos`, `melhorias`, `atividades`, `empresas`, `contatos`, `documentos`, `usuarios`
- Edge Functions: `auth-admin` (gestão de usuários), `airtable-sync` (sincronização periódica com deleções)
- Sincronização bidirecional Airtable ↔ Supabase com checagem de deleções a cada 30 minutos
- Storage de avatars configurado em `/storage/v1/object/public/avatars/`
