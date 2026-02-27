# Projeto de Conclusão - NoSQL

## 📚 Sobre o Projeto

Este repositório contém o material completo para aplicação de teste prático de MongoDB na disciplina de **Sistemas de Bancos de Dados NoSQL** para cursos de pós-graduação/MBA em Big Data.

## 🎯 Objetivo

Avaliar conhecimentos práticos em:
- Consultas MongoDB (find, filtros, projeções)
- Pipelines de agregação
- Operadores de agregação ($group, $match, $project, $lookup, $unwind)
- Análise de dados usando MongoDB Compass
- Boas práticas em NoSQL

## 📦 Estrutura do Repositório

```
mongodb-nosql-exam/
├── README.md                 # Este arquivo
├── exame/                    # Arquivos do exame para os alunos
│   ├── PROVA.md             # Enunciado completo do teste
│   ├── INSTRUCOES.md        # Instruções detalhadas
│   └── template-resposta.md # Template para entrega
├── scripts/                  # Scripts auxiliares
│   ├── setup-database.js    # Script de verificação do banco
│   └── validate-answers.js  # Script de validação
├── docs/                     # Documentação adicional
│   └── GUIA-COMPASS.md      # Guia de uso do Compass
└── datasets/                 # Informações sobre o dataset
    └── SAMPLE-MFLIX.md      # Descrição do sample_mflix
```

## 🚀 Pré-requisitos

### Para Aplicação do Teste
- MongoDB Community Edition 6.0+ ou MongoDB Atlas
- MongoDB Compass (última versão)
- Base de dados `sample_mflix` carregada

### Para os Alunos
- MongoDB Compass instalado e configurado
- Acesso ao cluster com a base `sample_mflix`
- Editor de texto para documentar as queries

## 📋 Como Usar Este Material

### Para Alunos

1. **Preparação do Ambiente**
   ```bash
   # Clone o repositório
   git clone https://github.com/seu-usuario/mongodb-nosql-exam.git
   cd mongodb-nosql-exam
   ```

2. **Configure o Banco de Dados**
   - Certifique-se que o sample_mflix está carregado
   - Execute o script de validação:
   ```bash
   mongosh < scripts/setup-database.js
   ```

3. **Resolução do Teste**
   - Acesse a pasta `exame/`
   - Leia atentamente `INSTRUCOES.md`
   - Resolva as questões em `PROVA.md`
   - Documente suas respostas usando `template-resposta.md`

## 🎓 Informações do Teste

- **Questões:** 5 (valor: 20 pontos cada)
- **Total:** 100 pontos
- **Tipo:** Prático individual
- **Ferramentas:** MongoDB Compass + Compass Shell
- **Consulta:** Documentação oficial permitida

## 📊 Distribuição de Pontos

| Questão | Tema | Pontos |
|---------|------|--------|
| Q1 | Consultas básicas com filtros | 20 |
| Q2 | Agregação com agrupamento | 20 |
| Q3 | Pipeline com $unwind e $group | 20 |
| Q4 | Agregação com $lookup | 20 |
| Q5 | Agregação com múltiplos estágios | 20 |

## 🔗 Recursos Adicionais

- [Documentação MongoDB](https://docs.mongodb.com/)
- [MongoDB Compass](https://www.mongodb.com/products/compass)
- [Aggregation Pipeline](https://docs.mongodb.com/manual/core/aggregation-pipeline/)
- [Sample Databases](https://docs.atlas.mongodb.com/sample-data/)

## 📝 Licença

Este material é disponibilizado para fins educacionais.

## 👨‍🏫 Autor

Desenvolvido para disciplinas de NoSQL em cursos de pós-graduação em Big Data.

---

**Versão:** 1.0  
**Última atualização:** Fevereiro 2025
