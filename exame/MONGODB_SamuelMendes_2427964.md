# RESPOSTAS - TESTE DE MONGODB

## IDENTIFICAÇÃO

**Nome completo:** Samuel Mendes da Silva  
**Matrícula:** 2427964
**Email:** samuelmds16@gmail.com
**Data:** 28/02/2026

---

## QUESTÃO 1 - Consulta Básica com Filtros

### Comando Utilizado
```javascript

db.movies.find(
  {
    $and: [
      { genres: { $in: ["Drama"] } },
      { year: { $gte: 2010 } },
      { year: { $lte: 2015 } },
      { "imdb.rating": { $gt: 7.5 } }
    ]
  },
  {
    title: 1,
    year: 1,
    "imdb.rating": 1,
    genres: 1,
    _id: 0
  }
).sort({ "imdb.rating": -1 }).limit(20)

```

### Resultado Obtido
- **Quantidade de documentos encontrados:** 352
- **5 primeiros filmes (título e rating):**
  1. Drishyam 8.9
  2. Most Likely to Succeed 8.9
  3. Kaakkaa Muttai 8.8
  4. Killswitch 8.8
  5. The Great Alone 8.7

### Screenshot
<img width="634" height="815" alt="Q1" src="https://github.com/user-attachments/assets/71d85219-1b76-4774-b899-1aee414aabae" />

### Observações (opcional)
Como estou conectado via terminal contei usando:
```
db.movies.countDocuments({
  genres: { $in: ["Drama"] },
  year: { $gte: 2010, $lte: 2015 },
  "imdb.rating": { $gt: 7.5 }
})
```
---

## QUESTÃO 2 - Agregação com Agrupamento

### Pipeline Utilizada
```javascript
db.movies.aggregate([
  {
    $match: {
      "countries.0": { $exists: true }  // ignora filme sem país
    }
  },
  { $unwind: "$countries" },
  {
    $group: {
      _id: "$countries",
      filmes: { $sum: 1 }
    }
  },
  { $sort: { filmes: -1 } },
  { $limit: 10 }
])
```

### Resultado Obtido

| Posição | País       | Quantidade de Filmes |
|---------|------------|----------------------|
| 1       | USA        | 10921                |
| 2       | UK         | 2652                 |
| 3       | France     | 2647                 |
| 4       | Germany    | 1494                 |
| 5       | Canada     | 1260                 |
| 6       | Italy      | 1217                 |
| 7       | Japan      | 786                  |
| 8       | Spain      | 675                  |
| 9       | India      | 564                  |
| 10      | Australia  | 470                  |

### Screenshot
<img width="1875" height="1200" alt="Q2" src="https://github.com/user-attachments/assets/60a95b27-d0df-404c-91a9-fc0b3e00ad6a" />

### Observações (opcional)

Primeiro tentei agrupar direto sem o unwind, deu errado porque o array inteiro virava a chave do grupo e era tratado como um país só, ai saquei que precisava explodir o array antes.

---

## QUESTÃO 3 - Pipeline com $unwind e $group

### Pipeline Utilizada
```javascript
db.movies.aggregate([
  {
    $match: {
      cast: { $exists: true },
      "imdb.rating": { $exists: true }
    }
  },
  { $unwind: "$cast" },
  {
    $group: {
      _id: "$cast",
      totalFilmes: { $sum: 1 },
      mediaRating: { $avg: "$imdb.rating" }
    }
  },
  { $sort: { totalFilmes: -1 } },
  { $limit: 5 },
  {
    $project: {
      _id: 0,
      ator: "$_id",
      totalFilmes: 1,
      mediaRating: { $round: ["$mediaRating", 2] }
    }
  }
])
```

### Resultado Obtido

| Posição | Ator                | Qtd Filmes | Rating Médio |
|---------|---------------------|------------|--------------|
| 1       | Gèrard Depardieu    | 67         | 6.69         |
| 2       | Robert De Niro      | 58         | 6.96         |
| 3       | Michael Caine       | 51         | 6.71         |
| 4       | Bruce Willis        | 49         | 6.41         |
| 5       | Samuel L. Jackson   | 48         | 6.40         |

### Screenshot
<img width="1920" height="1200" alt="Q3" src="https://github.com/user-attachments/assets/b6d3708e-407e-472e-9e46-1dfa8432537e" />

### Observações (opcional)

O enunciado pede para considerar apenas filmes que tenham rating definido, então adicionei um $match inicial com $exists: true antes de entrar na pipeline principal. filtrei filmes sem elenco pra não processar documento inútil

---

## QUESTÃO 4 - Agregação com $lookup

### Pipeline Utilizada
```javascript
db.comments.aggregate([
  {
    $group: {
      _id: "$movie_id",
      qtdComentarios: { $sum: 1 },
      // firstn limita a 3 no agrupamento, sem acumular
      primeirosUsuarios: {
        $firstN: {
          input: { nome: "$name", email: "$email" },
          n: 3
        }
      }
    }
  },
  { $sort: { qtdComentarios: -1 } },
  { $limit: 5 },
  // lookup só roda aqui, em cima dos 6
  {
    $lookup: {
      from: "movies",
      localField: "_id",
      foreignField: "_id",
      as: "filme"
    }
  },
  { $unwind: "$filme" },
  {
    $project: {
      _id: 0,
      titulo: "$filme.title",
      ano: "$filme.year",
      qtdComentarios: 1,
      primeirosUsuarios: 1
    }
  }
])
```

### Resultado Obtido

**Filme 1:**
- Título: The Taking of Pelham 1 2 3
- Ano: 2009
- Quantidade de comentários: 161
- Primeiros 3 usuários:
  1. Nome: Alliser Thorne | Email: owen_teale@gameofthron.es
  2. Nome: Amy Ramirez | Email: amy_ramirez@fakegmail.com
  3. Nome: Amy Ramirez | Email: amy_ramirez@fakegmail.com

**Filme 2:**
- Título: Ocean's Eleven
- Ano: 2001
- Quantidade de comentários: 158
- Primeiros 3 usuários:
  1. Nome: Amy Phillips | Email: amy_phillips@fakegmail.com
  2. Nome: Anthony Hurst | Email: anthony_hurst@fakegmail.com
  3. Nome: Anthony Hurst | Email: anthony_hurst@fakegmail.com

**Filme 3:**
- Título: About a Boy
- Ano: 2002
- Quantidade de comentários: 158
- Primeiros 3 usuários:
  1. Nome: Amy Phillips | Email: amy_phillips@fakegmail.com
  2. Nome: Anthony Cline | Email: anthony_cline@fakegmail.com
  3. Nome: Anthony Smith | Email: anthony_smith@fakegmail.com

**Filme 4:**
- Título: 50 First Dates
- Ano: 2004
- Quantidade de comentários: 158
- Primeiros 3 usuários:
  1. Nome: Alliser Thorne | Email: owen_teale@gameofthron.es
  2. Nome: Alliser Thorne | Email: owen_teale@gameofthron.es
  3. Nome: Amy Ramirez | Email: amy_ramirez@fakegmail.com

**Filme 5:**
- Título: Terminator Salvation
- Ano: 2009
- Quantidade de comentários: 158
- Primeiros 3 usuários:
  1. Nome: Amy Phillips | Email: amy_phillips@fakegmail.com
  2. Nome: Amy Phillips | Email: amy_phillips@fakegmail.com
  3. Nome: Amy Phillips | Email: amy_phillips@fakegmail.com

### Screenshot
<img width="1564" height="814" alt="Q4" src="https://github.com/user-attachments/assets/8343a161-5d7c-4c85-bd66-cfd0c2473571" />

### Observações (opcional)

Primeira tentativa foi fazer o $lookup sem filtro previo, travou. (provavelmente porque cruzou todos x todos entre filme e comentario)
Tentei inverter a logica e partir dos comentarios, mas deu erro de memoria, o group com push acumulava todos comentarios na memoria.
Tentei passar o parametro para usar a memoria de disco na agregaçao mas o free tier do atlas não permite.
Finalmente, decidi usar o firstn no lugar do push assim o mongo guarda só os 3 que quero e descarta o restante durante agrupamento.
Além disso, como citei antes decidi partir dos comentarios, porque o lookup só roda depois do limit, buscando as info apenas dos 5 filmes em vez de cruzar as coleções completas.

---

## QUESTÃO 5 - Agregação com Múltiplos Estágios

### Pipeline Utilizada
```javascript
db.movies.aggregate([
  {
    $match: {
      "imdb.rating": { $exists: true },
      genres: { $exists: true }
    }
  },
  { $unwind: "$genres" },
  {
    $group: {
      _id: "$genres",
      qtd: { $sum: 1 },
      media: { $avg: "$imdb.rating" }
    }
  },
  // critérios do "subestimado" aplicados após o agrupamento
  {
    $match: {
      qtd: { $gte: 10, $lte: 50 },
      media: { $gt: 7.0 }
    }
  },
  { $sort: { media: -1 } },
  {
    $project: {
      _id: 0,
      genero: "$_id",
      qtdFilmes: "$qtd",
      mediaIMDB: { $round: ["$media", 2] }
    }
  }
])
```

### Resultado Obtido

| Gênero | Qtd Filmes | Rating Médio |
|--------|------------|--------------|
| News   | 44         | 7.25         |

### Explicação
**Por que esses gêneros são considerados subestimados?**

Porque gêneros com quantidade entre 10 a 50 são nichos que a indústria não aposta muito. Mas quando esses filmes são feitos, o público avalia bem, daí a média alta.

Diferente de um gênero que aparece 2 vezes na base com nota boa, um gênero com 10 a 50 filmes e média acima de 7.0 mostra um padrão consistente de qualidade, tipo "esse gênero é bom, mas ninguém financia", muito provavelmente porque apesar de agradar seu público, o número de consumidores deve ser baixo.

### Observações

Rodei a query a primeira vez e só retornou 1 registro, fiz outra sem as restrições de faixa pra entender a distribuição. A base só tem 1 gênero entre 10 e 50 filmes, o restante é ou muito rara (< 10) ou muito comum (> 50). O resultado de apenas 1 gênero é esperado dado esses parametros.


### Screenshot
<img width="645" height="58" alt="Q5" src="https://github.com/user-attachments/assets/c51a65e6-7667-4368-8c3b-cf75b0a850d8" />

---
