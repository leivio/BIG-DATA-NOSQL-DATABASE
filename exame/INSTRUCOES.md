# INSTRUÇÕES PARA O TESTE DE MONGODB

## 📋 Antes de Começar

### 1. Verificação do Ambiente

Certifique-se de que você tem:

- [ ] MongoDB Compass instalado e funcionando
- [ ] Conexão estabelecida com o servidor MongoDB
- [ ] Base de dados `sample_mflix` carregada e acessível
- [ ] Editor de texto para documentar suas respostas

### 2. Verificando a Base de Dados

Execute os seguintes comandos no Compass Shell para verificar:

```javascript
// Listar databases disponíveis
show dbs

// Conectar ao sample_mflix
use sample_mflix

// Verificar collections disponíveis
show collections

// Deve exibir: comments, movies, sessions, theaters, users

// Contar documentos na collection movies
db.movies.countDocuments()
// Resultado esperado: aproximadamente 23,000 documentos

// Contar documentos na collection comments
db.comments.countDocuments()
// Resultado esperado: aproximadamente 50,000 documentos
```

Se alguma verificação falhar, **avise o professor imediatamente**.

---

## 🚀 Durante o Teste

### Como Usar o MongoDB Compass

#### Opção 1: Interface Gráfica (Aggregation Builder)

1. Selecione a collection no painel esquerdo
2. Clique na aba **"Aggregations"**
3. Clique em **"Add Stage"** para adicionar estágios
4. Selecione o operador ($match, $group, $project, etc.)
5. Digite o código JSON no editor
6. Clique em **"Export to Language"** > **"JavaScript"** para obter o código

#### Opção 2: Compass Shell (MongoSH)

1. Clique no ícone `>_MONGOSH` no rodapé do Compass
2. Digite seus comandos diretamente:

```javascript
// Exemplo de consulta simples
db.movies.find({ year: 2010 })

// Exemplo de agregação
db.movies.aggregate([
  { $match: { year: 2010 } },
  { $group: { _id: "$rated", count: { $sum: 1 } } }
])
```

### Estrutura das Collections

#### Collection: movies

Campos principais:
```javascript
{
  _id: ObjectId,
  title: String,           // Título do filme
  year: Number,           // Ano de lançamento
  rated: String,          // Classificação (PG, R, etc.)
  runtime: Number,        // Duração em minutos
  genres: [String],       // Array de gêneros
  directors: [String],    // Array de diretores
  cast: [String],         // Array de atores
  countries: [String],    // Array de países
  plot: String,           // Sinopse
  imdb: {                 // Dados do IMDB
    rating: Number,       // Nota (0-10)
    votes: Number         // Quantidade de votos
  },
  tomatoes: {             // Dados do Rotten Tomatoes
    viewer: {
      rating: Number
    }
  }
}
```

#### Collection: comments

Campos principais:
```javascript
{
  _id: ObjectId,
  name: String,           // Nome do usuário
  email: String,          // Email do usuário
  movie_id: ObjectId,     // Referência ao filme
  text: String,           // Texto do comentário
  date: ISODate           // Data do comentário
}
```

---

## 📝 Documentando Suas Respostas

### Formato Esperado para Cada Questão

```markdown
## QUESTÃO X

### Comando/Pipeline Utilizado
```javascript
// Cole aqui o código completo
db.collection.aggregate([
  { $match: { ... } },
  { $group: { ... } }
])
```

### Resultado Obtido
- Quantidade de documentos: XX
- Principais valores encontrados: ...

### Screenshot
[Anexar imagem aqui ou indicar arquivo separado]

### Observações (se aplicável)
- Dificuldades encontradas
- Decisões técnicas tomadas
```

### Salvando Seus Comandos

**Método 1: Copiar do Aggregation Builder**
1. Monte sua pipeline no Compass
2. Clique em "Export to Language"
3. Selecione "JavaScript"
4. Copie o código gerado

**Método 2: Copiar do Shell**
1. Digite o comando no MongoSH
2. Selecione e copie (Ctrl+C / Cmd+C)
3. Cole no seu arquivo de respostas

### Capturando Screenshots

- **Windows:** Use a Ferramenta de Captura ou tecle `Win + Shift + S`
- **Mac:** Use `Cmd + Shift + 4`
- **Linux:** Use `Print Screen` ou ferramenta Flameshot

Salve as imagens com nomes descritivos: `questao01-resultado.png`

---

## ⚠️ Dicas Importantes

### Boas Práticas

1. **Teste incremental:** Execute estágios da pipeline um a um
2. **Use .pretty():** Para formatar resultados no shell: `db.movies.find().pretty()`
3. **Limite resultados:** Use `.limit(5)` durante testes para não sobrecarregar
4. **Comente seu código:** Explique etapas complexas com comentários

### Operadores Mais Utilizados

**Agregação:**
- `$match` - Filtrar documentos
- `$group` - Agrupar dados
- `$project` - Selecionar/transformar campos
- `$sort` - Ordenar resultados
- `$limit` - Limitar quantidade
- `$unwind` - Separar arrays
- `$lookup` - Join entre collections

**Expressões:**
- `$sum` - Somar valores
- `$avg` - Calcular média
- `$max` / `$min` - Máximo e mínimo
- `$push` - Adicionar a array
- `$first` / `$last` - Primeiro ou último valor

### Debugging

Se algo não funcionar:

1. **Verifique a sintaxe:** Chaves, colchetes e vírgulas
2. **Teste cada estágio:** Comente estágios e teste um por vez
3. **Use $limit(1):** Para ver estrutura do documento
4. **Consulte documentação:** Sempre permitido!

```javascript
// Ver estrutura de um documento
db.movies.findOne()

// Ver campos disponíveis
db.movies.findOne({}, { _id: 0 })
```

---

## 🔍 Recursos Permitidos

### ✅ Permitido

- Documentação oficial do MongoDB (docs.mongodb.com)
- MongoDB Compass e todas suas funcionalidades
- Editor de texto local
- Anotações pessoais (caderno, papel)

### ❌ NÃO Permitido

- Comunicação com outros alunos
- Uso de IA ou assistentes de código (ChatGPT, Copilot, etc.)
- Consulta a respostas prontas na internet
- Compartilhamento de código durante o teste

---

## 📤 Entrega ( ver SEND_EXAM.md )

### Checklist Final

Antes de entregar, verifique:

- [ ] Todas as 5 questões respondidas
- [ ] Códigos completos e testados
- [ ] Screenshots incluídos onde solicitado
- [ ] Arquivo nomeado corretamente: `MONGODB_SeuNome_Matricula.md`
- [ ] Identificação preenchida no topo do arquivo

### Formato de Entrega

Use o arquivo `template-resposta.md` como base e preencha com suas respostas.

**Formatos aceitos:**
- Markdown (.md) - **preferencial**
- PDF (.pdf) - se incluir screenshots
- ZIP (.zip) - se screenshots forem arquivos separados

---

## 🆘 Problemas Técnicos

Se encontrar problemas durante o teste:

1. **Compass travou:** Feche e reabra o aplicativo
2. **Conexão perdida:** Reconecte ao servidor
3. **Query muito lenta:** Adicione `.limit(10)` temporariamente
4. **Erro de sintaxe:** Verifique vírgulas e chaves

**Se o problema persistir, avise o professor imediatamente.**

---

## 💡 Mensagem Final

- Leia cada questão com atenção
- Comece pelas questões que você acha mais fáceis
- Não perca muito tempo em uma questão - vá para a próxima e volte depois
- Documente seu raciocínio - mesmo que não complete a questão, explique sua abordagem
- Mantenha a calma e faça o seu melhor!

**Boa prova! 🚀**
