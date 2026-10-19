# Evidências de inspeção estática e banco

Verificações realizadas em 19/10/2026 sobre o arquivo SQLite incluído no ZIP e os arquivos-fonte.

| ID | Caso | Método | Resultado | Observação |
|---|---|---|---|---|
| CT01 | Existência das quatro tabelas | Consulta SQLite sqlite_master | PASSOU | usuarios, sqlite_sequence, clientes, veiculos, agendamentos |
| CT02 | Quantidade inicial em usuarios | SELECT COUNT(*) | PASSOU | 3 registros (esperado 3) |
| CT03 | Quantidade inicial em clientes | SELECT COUNT(*) | PASSOU | 3 registros (esperado 3) |
| CT04 | Quantidade inicial em veiculos | SELECT COUNT(*) | PASSOU | 4 registros (esperado 4) |
| CT05 | Quantidade inicial em agendamentos | SELECT COUNT(*) | PASSOU | 4 registros (esperado 4) |
| CT06 | FK veículos -> clientes | PRAGMA foreign_key_list(veiculos) | PASSOU | [(0, 0, 'clientes', 'cliente_id', 'id', 'NO ACTION', 'NO ACTION', 'NONE')] |
| CT07 | FK agendamentos -> veículos | PRAGMA foreign_key_list(agendamentos) | PASSOU | [(0, 0, 'veiculos', 'veiculo_id', 'id', 'NO ACTION', 'NO ACTION', 'NONE')] |
| CT08 | Unicidade da placa declarada no esquema | Inspeção de oficina_db.sql | PASSOU | UNIQUE declarado na coluna placa |
| CT09 | Hash bcrypt usado no login | Inspeção de server.js | PASSOU | Comparação com bcrypt.compareSync |
| CT10 | Sessão expira em 30 minutos | Inspeção de server.js | PASSOU | maxAge configurado para 30 minutos |
| CT11 | Rotas de dados usam middleware de login | Inspeção de server.js | PASSOU | Rotas consultadas incluem exigirLogin |
| CT12 | CPF usa AES-256-GCM | Inspeção de seguranca.js | PASSOU | Algoritmo AES-256-GCM declarado |
| CT13 | Escape de HTML no front-end | Inspeção de comum.js | PASSOU | Função esc() codifica caracteres HTML |
| CT14 | Placa é normalizada para maiúsculas | Inspeção de server.js | PASSOU | Normalização e regex presentes |
| CT15 | Validação rejeita data impossível | Inspeção de server.js | PASSOU | Validação compara data ISO de retorno |
| CT16 | Agendamentos incluem JOIN com veículos e clientes | Inspeção de server.js | PASSOU | Consulta possui os dois JOINs |
| CT17 | Busca de clientes contempla nome/e-mail/telefone/CPF | Inspeção de server.js | PASSOU | Quatro campos contemplados no filtro |
