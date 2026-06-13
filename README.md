# RPAS Offshore Ranking
### Sistema de Ranking Operacional de Pilotos RPAS para P&G

---

## Sobre o projeto

Sistema full-stack para ranquear pilotos RPAS offshore com base em critérios técnicos e operacionais reais. Desenvolvido com foco na realidade das operações em plataformas offshore nas Bacias de Campos e Santos.

**Stack:**
- Backend: FastAPI + SQLite (Python 3.10+)
- Frontend: HTML5 + CSS3 + JavaScript Vanilla
- Gráficos: Chart.js 4.4

---

## Critérios de Score

O score (0–100 pontos) é calculado por:

| Componente | Peso | Descrição |
|---|---|---|
| Técnica de voo | 25% | Precisão, controle de aeronave, manobras |
| Segurança | 25% | Cumprimento de procedimentos, avaliação de risco |
| Regulatório | 15% | ANAC, DECEA, SARPAS, NR-34 |
| Adaptabilidade | 15% | Condições adversas, imprevistos, multi-missão |
| Trabalho em equipe | 10% | Integração com tripulação, comunicação |
| Dom. equipamentos | 10% | M300, M350, M30T, payload, RTK |

**Bônus:**
- Experiência: +0.8 pts/ano (máx. 12 pts)
- Horas de voo: +1 pt a cada 500h (máx. 8 pts)
- Certificações: +1.5 pts por certificação ativa

**Penalidade:**
- Incidentes registrados: -3 pts por ocorrência

**Níveis:**
| Score | Nível |
|---|---|
| 90–100 | 🔶 Elite |
| 80–89 | 🟢 Sênior |
| 65–79 | 🔵 Pleno |
| < 65 | ⚪ Júnior |

---

## Instalação e execução

```bash
# 1. Instalar dependências
pip install -r requirements.txt

# 2. Iniciar (Linux/Mac)
chmod +x start.sh && ./start.sh

# 3. Ou manualmente:
cd backend
uvicorn main:app --reload --port 8000

# 4. Abrir o frontend
# Opção A: direto no navegador (arquivo)
#   Abra frontend/index.html

# Opção B: servidor local
cd frontend && python -m http.server 3000
# Acesse http://localhost:3000
```

---

## Estrutura do projeto

```
rpas-ranking/
├── backend/
│   ├── main.py              # Entrypoint FastAPI
│   ├── database.py          # Banco SQLite + seed
│   └── routers/
│       ├── pilotos.py       # CRUD pilotos + score
│       ├── voos.py          # Registro de voos
│       ├── incidentes.py    # Registro de incidentes
│       ├── relatorios.py    # Relatório consolidado
│       └── auth.py          # Autenticação
├── frontend/
│   ├── index.html           # Ranking principal
│   ├── piloto.html          # Perfil individual
│   ├── relatorio.html       # Relatório da frota
│   ├── css/style.css        # Design system
│   └── js/
│       ├── app.js           # Lógica do ranking
│       ├── piloto.js        # Lógica do perfil
│       └── relatorio.js     # Lógica dos gráficos
├── requirements.txt
└── start.sh
```

---

## API Endpoints

```
GET  /api/pilotos/ranking         → Ranking completo com scores
GET  /api/pilotos/{id}            → Perfil detalhado do piloto
POST /api/pilotos/                → Cadastrar novo piloto
PUT  /api/pilotos/{id}/competencias → Atualizar competências
POST /api/pilotos/{id}/certificacoes → Adicionar certificação
POST /api/pilotos/{id}/aeronaves  → Adicionar aeronave habilitada

POST /api/voos/                   → Registrar voo
GET  /api/voos/piloto/{id}        → Histórico de voos
GET  /api/voos/stats/{id}         → Estatísticas de voo

POST /api/incidentes/             → Registrar incidente
GET  /api/incidentes/piloto/{id}  → Incidentes do piloto
PUT  /api/incidentes/{id}/encerrar → Encerrar incidente

GET  /api/relatorios/resumo       → Resumo geral da frota

POST /api/auth/login              → Login (admin/admin123)
```

Documentação interativa disponível em: `http://localhost:8000/docs`

---

## Créditos

Desenvolvido por **William Oliveira** (TheDevOffshore)  
Piloto RPAS Offshore · Dev Full-Stack · São José dos Campos, SP
