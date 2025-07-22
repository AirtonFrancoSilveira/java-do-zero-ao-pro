# Exercícios Práticos: Estruturas de Dados Java

Este arquivo contém exercícios práticos progressivos que consolidam o conhecimento sobre `List`, `Map` e `Set`. Os exercícios estão organizados por nível de dificuldade e cobrem desde conceitos básicos até otimizações avançadas de performance.

---

## 🟢 Nível Básico: Fundamentos

### Exercício 1: Escolha da Estrutura Correta
**Objetivo:** Treinar a escolha da estrutura de dados mais adequada para cada cenário.

**Cenários:**
1. Armazenar uma lista de tarefas onde a ordem de criação é importante
2. Manter um cache de usuários logados (busca rápida por ID)
3. Armazenar configurações de sistema mantendo a ordem de inserção
4. Lista de produtos únicos em um carrinho de compras
5. Fila de processamento de pedidos (FIFO)
6. Ranking de jogadores (sempre ordenado por pontuação)

**Sua Resposta:**
```java
// 1. Lista de tarefas com ordem de criação:
// Resposta: ________________

// 2. Cache de usuários (busca rápida por ID):
// Resposta: ________________

// 3. Configurações mantendo ordem de inserção:
// Resposta: ________________

// 4. Produtos únicos no carrinho:
// Resposta: ________________

// 5. Fila FIFO de pedidos:
// Resposta: ________________

// 6. Ranking ordenado por pontuação:
// Resposta: ________________
```

### Exercício 2: Implementação Básica
**Objetivo:** Praticar operações básicas com diferentes estruturas.

**Tarefa:** Implemente um sistema simples de biblioteca que:
- Mantém uma lista de livros disponíveis (pode ter duplicatas)
- Mantém um conjunto de usuários únicos
- Mapeia cada usuário aos livros que ele emprestou

```java
public class BibliotecaSimples {
    // TODO: Declare as estruturas de dados adequadas
    
    public void adicionarLivro(String titulo) {
        // TODO: Implementar
    }
    
    public void cadastrarUsuario(String nome) {
        // TODO: Implementar
    }
    
    public boolean emprestarLivro(String usuario, String livro) {
        // TODO: Implementar
        // Retorna true se o empréstimo foi realizado com sucesso
    }
    
    public Set<String> livrosEmprestadosPor(String usuario) {
        // TODO: Implementar
    }
    
    public int totalLivrosDisponiveis() {
        // TODO: Implementar
    }
}
```

---

## 🟡 Nível Intermediário: Otimizações e Padrões

### Exercício 3: Análise de Performance
**Objetivo:** Comparar performance entre diferentes implementações.

**Tarefa:** Implemente e compare os tempos de execução das seguintes operações:

```java
public class AnalisePerformance {
    
    public static void compararInserecaoInicio() {
        List<Integer> arrayList = new ArrayList<>();
        List<Integer> linkedList = new LinkedList<>();
        
        // TODO: Meça o tempo para inserir 10.000 elementos no INÍCIO de cada lista
        // Use System.nanoTime() para medir
        
        System.out.println("ArrayList - Inserção no início: ___ms");
        System.out.println("LinkedList - Inserção no início: ___ms");
    }
    
    public static void compararAcessoAleatorio() {
        // TODO: Compare o tempo de acesso aleatório (get) em ArrayList vs LinkedList
        // Use listas com 10.000 elementos e faça 1.000 acessos aleatórios
    }
    
    public static void compararBuscaEmSet() {
        // TODO: Compare contains() em HashSet vs TreeSet vs ArrayList
        // Use 10.000 elementos e faça 1.000 buscas
    }
}
```

### Exercício 4: Sistema de Cache LRU
**Objetivo:** Implementar um cache LRU usando LinkedHashMap.

```java
public class CacheLRU<K, V> {
    private final int capacidade;
    private final Map<K, V> cache;
    
    public CacheLRU(int capacidade) {
        this.capacidade = capacidade;
        // TODO: Inicializar LinkedHashMap com comportamento LRU
        // Dica: Use o construtor com accessOrder = true
    }
    
    public V get(K chave) {
        // TODO: Implementar get que move elemento para o final (mais recente)
    }
    
    public void put(K chave, V valor) {
        // TODO: Implementar put que remove o elemento menos usado quando necessário
    }
    
    public int tamanho() {
        return cache.size();
    }
}
```

### Exercício 5: Operações de Conjunto Avançadas
**Objetivo:** Implementar operações matemáticas com Sets.

```java
public class OperacoesConjunto {
    
    public static <T> Set<T> uniao(Set<T> conjunto1, Set<T> conjunto2) {
        // TODO: Implementar união eficiente
    }
    
    public static <T> Set<T> intersecao(Set<T> conjunto1, Set<T> conjunto2) {
        // TODO: Implementar interseção eficiente
        // Dica: Sempre itere sobre o conjunto menor
    }
    
    public static <T> Set<T> diferenca(Set<T> conjunto1, Set<T> conjunto2) {
        // TODO: Implementar diferença (elementos em conjunto1 mas não em conjunto2)
    }
    
    public static <T> boolean saoDisjuntos(Set<T> conjunto1, Set<T> conjunto2) {
        // TODO: Verificar se os conjuntos não têm elementos em comum
        // Otimização: pare na primeira interseção encontrada
    }
    
    public static <T> Set<T> diferenciaSimetrica(Set<T> conjunto1, Set<T> conjunto2) {
        // TODO: Elementos que estão em um conjunto OU no outro, mas não em ambos
    }
}
```

---

## 🔴 Nível Avançado: Problemas Complexos

### Exercício 6: Sistema de Recomendação
**Objetivo:** Usar estruturas de dados para implementar um sistema de recomendação básico.

```java
public class SistemaRecomendacao {
    // Mapeia usuário -> conjunto de itens que ele gostou
    private Map<String, Set<String>> preferenciasUsuarios;
    
    // Mapeia item -> conjunto de usuários que gostaram
    private Map<String, Set<String>> itensPorUsuario;
    
    public SistemaRecomendacao() {
        // TODO: Inicializar as estruturas adequadas
    }
    
    public void adicionarPreferencia(String usuario, String item) {
        // TODO: Adicionar preferência mantendo os dois mapeamentos sincronizados
    }
    
    public Set<String> recomendarPara(String usuario) {
        // TODO: Implementar recomendação baseada em usuários similares
        // Algoritmo:
        // 1. Encontrar usuários com preferências similares
        // 2. Recomendar itens que eles gostaram mas o usuário atual não conhece
    }
    
    public List<String> usuariosSimilares(String usuario) {
        // TODO: Retornar lista de usuários ordenada por similaridade
        // Similaridade = número de itens em comum
    }
    
    public Map<String, Integer> estatisticasItem(String item) {
        // TODO: Retornar estatísticas do item
        // Ex: {"totalUsuarios": 150, "percentualPopularidade": 75}
    }
}
```

### Exercício 7: Análise de Texto Avançada
**Objetivo:** Combinar múltiplas estruturas para análise eficiente de texto.

```java
public class AnalisadorTexto {
    
    public static Map<String, Integer> contarPalavras(String texto) {
        // TODO: Contar frequência de palavras
        // Considere: case-insensitive, remover pontuação
    }
    
    public static List<String> palavrasMaisFrequentes(String texto, int top) {
        // TODO: Retornar as N palavras mais frequentes
        // Dica: Use TreeMap ou PriorityQueue para ordenação
    }
    
    public static Set<String> palavrasUnicas(List<String> textos) {
        // TODO: Encontrar palavras que aparecem em TODOS os textos
    }
    
    public static Map<Integer, Set<String>> agruparPorTamanho(String texto) {
        // TODO: Agrupar palavras por tamanho
        // Resultado: {3: {"cat", "dog"}, 4: {"word", "text"}, ...}
    }
    
    public static boolean saoAnagramas(String palavra1, String palavra2) {
        // TODO: Verificar se duas palavras são anagramas
        // Use estruturas de dados para otimizar
    }
    
    public static Map<Character, List<String>> indicePorPrimeiraLetra(List<String> palavras) {
        // TODO: Criar índice de palavras por primeira letra
        // Mantenha as listas ordenadas alfabeticamente
    }
}
```

### Exercício 8: Sistema de Monitoramento
**Objetivo:** Implementar um sistema que monitora métricas em tempo real.

```java
public class MonitorMetricas {
    // TODO: Escolher estruturas adequadas para:
    // - Armazenar métricas por timestamp
    // - Cache das últimas N métricas
    // - Índice rápido por tipo de métrica
    
    public void registrarMetrica(String tipo, double valor, long timestamp) {
        // TODO: Registrar nova métrica
    }
    
    public double mediaUltimasN(String tipo, int n) {
        // TODO: Calcular média das últimas N métricas de um tipo
    }
    
    public Map<String, Double> resumoUltimaHora() {
        // TODO: Retornar resumo (média, min, max) de cada tipo na última hora
    }
    
    public List<String> tiposComAnomalias(double threshold) {
        // TODO: Identificar tipos de métricas com valores anômalos
        // Anômalo = valor atual > threshold * média histórica
    }
    
    public void limparDadosAntigos(long timestampLimite) {
        // TODO: Remover métricas mais antigas que o timestamp limite
    }
}
```

---

## 🏆 Desafio Final: Sistema Completo

### Exercício 9: E-commerce Backend
**Objetivo:** Integrar todos os conceitos em um sistema real.

```java
public class EcommerceBackend {
    // TODO: Declare todas as estruturas necessárias
    
    // Gestão de Produtos
    public void adicionarProduto(String id, String nome, double preco, String categoria) {}
    public List<String> buscarProdutosPorCategoria(String categoria) {}
    public List<String> produtosMaisCaros(int limite) {}
    
    // Gestão de Usuários
    public void cadastrarUsuario(String id, String nome, String email) {}
    public boolean emailJaExiste(String email) {}
    
    // Carrinho de Compras
    public void adicionarAoCarrinho(String usuarioId, String produtoId, int quantidade) {}
    public double calcularTotalCarrinho(String usuarioId) {}
    public Map<String, Integer> obterCarrinho(String usuarioId) {}
    
    // Sistema de Recomendação
    public void registrarVisualizacao(String usuarioId, String produtoId) {}
    public List<String> recomendarProdutos(String usuarioId, int limite) {}
    
    // Análise e Relatórios
    public Map<String, Integer> produtosMaisVisualizados() {}
    public Set<String> usuariosAtivos(int ultimosDias) {}
    public double receitaTotalPorCategoria(String categoria) {}
    
    // Performance e Cache
    public void invalidarCache(String chave) {}
    public void otimizarIndices() {}
}
```

---

## 🔧 Gabarito e Dicas

### Respostas Exercício 1:
1. **ArrayList** - Ordem importa, acesso sequencial comum
2. **HashMap<String, Usuario>** - Busca O(1) por ID
3. **LinkedHashMap** - Preserva ordem de inserção
4. **HashSet** ou **LinkedHashSet** - Elementos únicos
5. **LinkedList** (como Queue) - FIFO eficiente
6. **TreeMap** ou **TreeSet** - Sempre ordenado

### Dicas Gerais:
- **Performance**: Sempre meça antes de otimizar
- **Memória**: Considere o overhead de cada estrutura
- **Concorrência**: Use implementações thread-safe quando necessário
- **Inicialização**: Defina capacidade inicial quando souber o tamanho aproximado

### Benchmarking Template:
```java
public static long medirTempo(Runnable operacao) {
    long inicio = System.nanoTime();
    operacao.run();
    long fim = System.nanoTime();
    return (fim - inicio) / 1_000_000; // Converter para ms
}
```

---

**Próximo Passo:** Após completar estes exercícios, você terá uma compreensão sólida e prática das estruturas de dados Java. O próximo arquivo abordará análise de performance e casos de uso específicos para situações do mundo real. 