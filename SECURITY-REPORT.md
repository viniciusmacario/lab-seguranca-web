#  2. SECURITY-REPORT.md (copia e cola)

```md
#  SECURITY REPORT

##  Aluno:
Vinicius Macario

---

#  FASE 1 — RECON

A API foi analisada via Swagger e foi possível identificar falhas de segurança relacionadas à validação de entrada, controle de acesso e exposição de dados.

---

#  FASE 2 — EXPLOIT

##  1. SQL Injection

**Endpoint:**
GET /api/produtos?nome=

**Exploit:**
' OR 1=1 --

**Impacto:**
Permite acesso indevido a dados do banco.

---

##  2. XSS Refletido

**Endpoint:**
GET /busca?q=

**Exploit:**
<script>alert('XSS')</script>

**Impacto:**
Execução de código malicioso no navegador.

---

##  3. IDOR

**Endpoint:**
GET /api/usuarios/{userId}/pedidos

**Exploit:**
Acessar outro ID:
Ex: /api/usuarios/1/pedidos

**Impacto:**
Acesso a dados de outros usuários.

---

##  4. Exposição de Dados

**Endpoint:**
GET /api/usuarios/{id}

**Problema:**
Retorna senha, token e role.

**Impacto:**
Risco de invasão de contas.

---

##  5. Missing Auth

**Problema:**
Endpoint administrativo sem restrição.

**Impacto:**
Usuários comuns acessam funções críticas.

---

#  FASE 3 — PATCH

##  SQL Injection
Uso de query segura (LINQ ou parâmetros)

## XSS
Escape de HTML

##  IDOR
Validação do usuário logado

##  Exposição de dados
Uso de DTO

##  Missing Auth
Uso de [Authorize(Roles = "Admin")]

---

#  FASE 4 — VERIFY

Após correções:
- SQL Injection não funciona
- XSS bloqueado
- Usuários não acessam dados alheios
- Dados sensíveis protegidos

---

# CONCLUSÃO

As vulnerabilidades identificadas representam riscos críticos. As correções aplicadas seguem boas práticas de segurança, garantindo maior proteção da aplicação.
