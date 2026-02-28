# RESPOSTAS - TESTE DE MONGODB

## IDENTIFICAÇÃO

**Nome completo:** _____________________________________________  
**Matrícula:** ____________________  
**Email:** ________________________________________  
**Data:** ___/___/______

---

## QUESTÃO 1 - Consulta Básica com Filtros

### Comando Utilizado
```javascript
// Cole aqui seu comando find()


```

### Resultado Obtido
- **Quantidade de documentos encontrados:** ______
- **5 primeiros filmes (título e rating):**
  1. 
  2. 
  3. 
  4. 
  5. 

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao01.png]_

### Observações (opcional)


---

## QUESTÃO 2 - Agregação com Agrupamento

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline de agregação
db.movies.aggregate([


])
```

### Resultado Obtido

| Posição | País | Quantidade de Filmes |
|---------|------|----------------------|
| 1º | | |
| 2º | | |
| 3º | | |
| 4º | | |
| 5º | | |
| 6º | | |
| 7º | | |
| 8º | | |
| 9º | | |
| 10º | | |

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao02.png]_

### Observações (opcional)


---

## QUESTÃO 3 - Pipeline com $unwind e $group

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline de agregação
db.movies.aggregate([


])
```

### Resultado Obtido

| Posição | Ator | Qtd Filmes | Rating Médio |
|---------|------|------------|--------------|
| 1º | | | |
| 2º | | | |
| 3º | | | |
| 4º | | | |
| 5º | | | |

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao03.png]_

### Observações (opcional)


---

## QUESTÃO 4 - Agregação com $lookup

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline com $lookup
db.movies.aggregate([


])
```

### Resultado Obtido

**Filme 1:**
- Título: 
- Ano: 
- Quantidade de comentários: 
- Primeiros 3 usuários:
  1. Nome: __________ | Email: __________
  2. Nome: __________ | Email: __________
  3. Nome: __________ | Email: __________

**Filme 2:**
- Título: 
- Ano: 
- Quantidade de comentários: 
- Primeiros 3 usuários:
  1. Nome: __________ | Email: __________
  2. Nome: __________ | Email: __________
  3. Nome: __________ | Email: __________

### Screenshot
_[Anexar screenshot ou indicar arquivo: questao04.png]_

### Observações (opcional)

---

## QUESTÃO 5 - Agregação com Múltiplos Estágios

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline completa
db.movies.aggregate([


])
```

### Resultado Obtido

| Gênero | Qtd Filmes | Rating Médio |
|--------|------------|--------------|
| | | |
| | | |
| | | |
| | | |

### Explicação
**Por que esses gêneros são considerados subestimados?**


### Screenshot
_[Anexar screenshot ou indicar arquivo: questao07.png]_

---
