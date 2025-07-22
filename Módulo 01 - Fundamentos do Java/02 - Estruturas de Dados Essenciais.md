# Capítulo 2: Estruturas de Dados Essenciais

Se a JVM é o coração do Java, as estruturas de dados são o sistema circulatório. Elas são fundamentais para organizar, armazenar e manipular dados de forma eficiente. A escolha da estrutura de dados correta é uma das decisões mais impactantes que um desenvolvedor pode tomar em termos de performance e clareza do código.

Em Java, o **Java Collections Framework** fornece um conjunto rico e maduro de interfaces e implementações de estruturas de dados. Vamos focar nas três interfaces mais importantes: `List`, `Set` e `Map`.

---

### 2.1. A Interface `List`: Coleções Ordenadas

Uma `List` é uma coleção **ordenada** que permite elementos **duplicados**. "Ordenada" aqui significa que os elementos são mantidos na ordem em que foram inseridos, e você pode acessá-los por um índice numérico (começando em zero), assim como em um array.

**Implementações Principais:**

*   `ArrayList`: Utiliza um array dinâmico internamente.
    *   **Pontos Fortes:** Acesso a elementos por índice é extremamente rápido (complexidade O(1)).
    *   **Pontos Fracos:** Adicionar ou remover elementos no meio da lista é lento (O(n)), pois pode exigir a reorganização de todos os elementos subsequentes.
    *   **Quando usar?** É a sua escolha padrão para uma lista. Use quando a principal operação for percorrer a lista ou acessar elementos por índice.

*   `LinkedList`: Utiliza uma lista duplamente encadeada. Cada elemento é um "nó" que guarda uma referência para o elemento anterior e o próximo.
    *   **Pontos Fortes:** Adicionar ou remover elementos no início ou no fim da lista é muito rápido (O(1)).
    *   **Pontos Fracos:** Acesso a um elemento por índice é lento (O(n)), pois precisa percorrer a lista desde o início ou o fim até encontrar o elemento. Consome mais memória que o `ArrayList`.
    *   **Quando usar?** Use quando você precisar realizar um grande número de inserções e remoções, especialmente nas extremidades da lista (funcionando como uma fila ou pilha).

**Exemplo Prático (Código):**

```java
// Criando uma lista de strings
List<String> nomes = new ArrayList<>();
nomes.add("Ana");
nomes.add("Carlos");
nomes.add("Ana"); // Duplicado é permitido

// Acesso rápido por índice
System.out.println("O primeiro nome é: " + nomes.get(0)); // Saída: Ana

// LinkedList para operações de fila
LinkedList<String> filaAtendimento = new LinkedList<>();
filaAtendimento.addLast("Cliente A");
filaAtendimento.addLast("Cliente B");
String proximo = filaAtendimento.removeFirst(); // Atende o primeiro cliente
```

---

### 2.2. A Interface `Set`: Coleções Únicas

Um `Set` é uma coleção que **não permite elementos duplicados**. Sua principal finalidade é garantir a unicidade dos seus elementos. A ordem não é garantida na maioria das implementações.

**Implementações Principais:**

*   `HashSet`: Utiliza uma tabela de hash internamente. É a implementação mais comum de `Set`.
    *   **Pontos Fortes:** Operações de adicionar, remover e verificar se um elemento existe (`contains`) são extremamente rápidas, em média O(1).
    *   **Pontos Fracos:** A ordem dos elementos não é garantida e pode parecer aleatória.
    *   **Quando usar?** Sempre que você precisar armazenar um conjunto de elementos únicos e a ordem não importar. Perfeito para remover duplicatas de uma outra coleção.

*   `LinkedHashSet`: Uma combinação de `HashSet` e `LinkedList`.
    *   **Pontos Fortes:** Mantém a performance do `HashSet` (O(1) para operações básicas) e **garante a ordem de inserção**.
    *   **Pontos Fracos:** Consome um pouco mais de memória que o `HashSet`.
    *   **Quando usar?** Quando você precisa de elementos únicos E se importa com a ordem em que foram adicionados.

*   `TreeSet`: Utiliza uma árvore (Red-Black Tree) para armazenar os elementos.
    *   **Pontos Fortes:** Mantém os elementos **ordenados** de acordo com sua "ordem natural" (alfabética, numérica) ou um `Comparator` fornecido.
    *   **Pontos Fracos:** As operações são mais lentas que no `HashSet`, com complexidade O(log n).
    *   **Quando usar?** Quando você precisa de um conjunto de elementos únicos que esteja sempre ordenado.

**Exemplo Prático (Código):**

```java
// Removendo duplicatas de uma lista
List<Integer> notasComDuplicatas = new ArrayList<>(List.of(10, 8, 9, 8, 7, 10));
Set<Integer> notasUnicas = new HashSet<>(notasComDuplicatas);
System.out.println(notasUnicas); // Saída (ordem não garantida): [7, 8, 9, 10]

// Mantendo a ordem de inserção
Set<String> tarefas = new LinkedHashSet<>();
tarefas.add("Comprar café");
tarefas.add("Escrever código");
tarefas.add("Revisar PR");
System.out.println(tarefas); // Saída: [Comprar café, Escrever código, Revisar PR]
```

---

### 2.3. A Interface `Map`: Estrutura Chave-Valor

Um `Map` é uma estrutura que armazena pares de **chave-valor**. Cada chave é única (assim como em um `Set`) e está associada a um valor. É a estrutura de dados ideal quando você precisa buscar um valor rapidamente através de um identificador único.

**Implementações Principais:**

*   `HashMap`: Utiliza uma tabela de hash. É a implementação mais comum e rápida.
    *   **Pontos Fortes:** Obter um valor a partir de uma chave é, em média, O(1).
    *   **Pontos Fracos:** A ordem das chaves não é garantida.
    *   **Quando usar?** É a sua escolha padrão para um `Map`. Use sempre que precisar de uma associação chave-valor rápida sem se preocupar com a ordem.

*   `LinkedHashMap`: Mantém a ordem de inserção das chaves.
    *   **Pontos Fortes:** Tão rápido quanto `HashMap` e mantém a ordem de inserção.
    *   **Quando usar?** Quando a ordem em que os pares foram adicionados é importante.

*   `TreeMap`: Mantém as chaves ordenadas.
    *   **Pontos Fortes:** As chaves estão sempre ordenadas.
    *   **Pontos Fracos:** Operações são mais lentas, O(log n).
    *   **Quando usar?** Quando você precisa iterar sobre as chaves de forma ordenada.

**Exemplo Prático (Código):**

```java
// Mapeando o ID de um usuário para seu nome
Map<Integer, String> usuarios = new HashMap<>();
usuarios.put(1, "Alice");
usuarios.put(20, "Bob");
usuarios.put(3, "Charlie");

// Buscando um usuário pelo ID
String nomeUsuario = usuarios.get(20);
System.out.println("O nome do usuário com ID 20 é: " + nomeUsuario); // Saída: Bob

// Verificando se uma chave existe
if (usuarios.containsKey(3)) {
    System.out.println("Charlie está no mapa.");
}
```

### 2.4. Qual usar e quando? (O Resumo do Mentor)

| Se você precisa...                               | Use...         | Por quê?                                                                                              |
| ------------------------------------------------ | -------------- | ----------------------------------------------------------------------------------------------------- |
| Uma lista simples, acesso rápido por posição.    | `ArrayList`    | Acesso O(1). É a lista de propósito geral mais eficiente.                                             |
| Muitas inserções/remoções nas pontas.           | `LinkedList`   | Operações O(1) no início/fim, ideal para filas (`Queue`) e pilhas (`Deque`).                          |
| Apenas garantir que não há itens duplicados.     | `HashSet`      | Extremamente rápido (O(1)) para verificar a existência de um item.                                    |
| Itens únicos E manter a ordem de inserção.       | `LinkedHashSet`| O melhor dos dois mundos: unicidade e ordem de inserção.                                              |
| Itens únicos E mantê-los sempre ordenados.       | `TreeSet`      | Garante a ordem natural (ou customizada), com um custo de performance (O(log n)).                    |
| Uma busca rápida por uma chave única.            | `HashMap`      | Acesso O(1) para buscar valores. É o `Map` de propósito geral.                                        |
| Busca rápida por chave E manter a ordem de inserção. | `LinkedHashMap`| Garante a ordem de iteração, útil para caches (como LRU) ou configurações que precisam ser lidas na ordem. |
| Busca por chave E iterar pelas chaves em ordem. | `TreeMap`      | Garante que as chaves estarão sempre ordenadas.                                                       |

**Recursos de Aprofundamento:**
*   **Vídeo:** [Collections em Java - DevDojo](https://www.youtube.com/watch?v=SI7k_i3G6iU)
*   **Artigo/Tutorial:** [Baeldung - The Java Collections Framework](https://www.baeldung.com/java-collections) (Baeldung é uma referência essencial para qualquer desenvolvedor Java)
*   **Documentação Oficial:** [Oracle - The Collections Framework](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/overview.html) (Apesar de ser da versão 8, os conceitos centrais são os mesmos e explicados de forma muito clara). 