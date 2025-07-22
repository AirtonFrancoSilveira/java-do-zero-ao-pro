# Capítulo 3: Orientação a Objetos na Prática

Bem-vindo ao pilar central do Java. A Orientação a Objetos (OO) é mais do que uma característica da linguagem; é um paradigma, uma forma de pensar sobre como estruturar seus programas. A ideia principal é trazer o mundo real, composto por objetos, para dentro do seu código.

Um **objeto** em Java possui duas características principais:
1.  **Estado:** Representado por seus atributos (variáveis). Ex: Um objeto `Carro` tem estado como `cor`, `velocidadeAtual`, `ligado`.
2.  **Comportamento:** Representado por seus métodos (funções). Ex: Um objeto `Carro` tem comportamentos como `ligar()`, `acelerar()`, `frear()`.

A **classe** é a planta, o molde a partir do qual os objetos são criados. A classe `Carro` define que todo carro terá uma cor e poderá ser acelerado. `meuFusca` e `suaFerrari` são **instâncias** (objetos) dessa classe, cada um com seu próprio estado (`cor="azul"` ou `cor="vermelho"`).

Vamos explorar os 4 pilares que sustentam este paradigma.

---

### 3.1. Encapsulamento: A Caixa-Preta Segura

**O que é?**
É o ato de agrupar os dados (atributos) e os métodos que operam nesses dados dentro de uma única unidade (a classe). Mais importante, o encapsulamento envolve **esconder os detalhes da implementação** do mundo exterior.

**Analogia:** Pense no controle remoto da sua TV. Você tem botões (uma interface pública) como `aumentarVolume()` e `trocarCanal()`. Você não sabe e não precisa saber como os circuitos internos funcionam para executar essas ações. O controle **encapsula** a complexidade.

**Como em Java?**
Usamos os modificadores de acesso. A prática mais comum é declarar os **atributos como `private`** e expor o acesso a eles através de **métodos públicos (`getters` e `setters`)**.

**Por que é importante?**
*   **Controle:** Você pode adicionar validações. O método `setVelocidade(int v)` pode impedir que alguém atribua uma velocidade negativa.
*   **Manutenibilidade:** Se você precisar mudar a forma como um atributo é armazenado internamente, só precisará mudar dentro da classe. O resto do mundo continuará usando o mesmo método `get` e `set`, sem quebrar o código.

**Exemplo Prático:**

```java
public class ContaBancaria {
    private double saldo; // Escondido, protegido.

    // Interface pública para interagir com o saldo
    public double getSaldo() {
        return this.saldo;
    }

    public void depositar(double valor) {
        if (valor > 0) {
            this.saldo += valor;
        }
    }

    public void sacar(double valor) {
        if (valor > 0 && this.saldo >= valor) {
            this.saldo -= valor;
        }
    }
}
```

---

### 3.2. Herança: Reutilizando e Especializando

**O que é?**
É um mecanismo que permite que uma classe (subclasse ou classe filha) herde atributos e métodos de outra classe (superclasse ou classe pai).

**Analogia:** Pense em veículos. Existe um conceito geral de `Veiculo` (tem `marca`, `modelo`, pode `acelerar`). Um `Carro` **é um** `Veiculo`, então ele herda tudo de `Veiculo`, mas adiciona coisas específicas, como `numeroDePortas`. Uma `Moto` também **é um** `Veiculo`, mas adiciona `cilindradas`.

**Como em Java?**
Usamos a palavra-chave `extends`.

**Por que é importante?**
*   **Reutilização de Código:** Você não precisa reescrever os atributos `marca` e `modelo` em todas as classes de veículos.
*   **Organização:** Cria uma hierarquia clara e lógica (um `Carro` É UM `Veiculo`).

**Exemplo Prático:**

```java
// Superclasse (Pai)
public class Funcionario {
    private String nome;
    protected double salario; // protected é visível para as classes filhas

    public void registrarPonto() {
        System.out.println("Ponto registrado para " + this.nome);
    }
}

// Subclasse (Filha)
public class Gerente extends Funcionario {
    private int senha;

    public void aprovarVerba() {
        // Lógica específica do gerente
    }
}
```
Um `Gerente` tem `nome`, `salario` e pode `registrarPonto()` (herdado), além de ter sua própria `senha` e o método `aprovarVerba()`.

---

### 3.3. Polimorfismo: Muitas Formas, Mesma Interface

**O que é?**
Poli (muitas) + morfismo (formas). É a capacidade de um objeto ser referenciado de múltiplas formas, geralmente tratando um objeto de uma classe filha como se fosse um objeto da classe pai. Frequentemente, isso se manifesta na **sobrescrita de métodos** (`@Override`).

**Analogia:** Imagine que você tem vários animais (`Cachorro`, `Gato`, `Pato`) e pede para cada um `fazerSom()`. A ação é a mesma, mas o resultado é diferente para cada um (um late, um mia, outro grasna). Você não precisa saber o tipo específico do animal para pedir que ele faça som.

**Como em Java?**
Uma subclasse pode fornecer uma implementação específica para um método que já é definido em sua superclasse.

**Por que é importante?**
*   **Flexibilidade e Desacoplamento:** Você pode escrever código que opera em objetos da superclasse, e ele funcionará automaticamente com qualquer nova subclasse que for criada, sem precisar de `if-else` para cada tipo.

**Exemplo Prático:**

```java
public abstract class FormaGeometrica { // abstract: não pode ser instanciada diretamente
    public abstract double calcularArea(); // método abstrato: deve ser implementado pelas filhas
}

public class Quadrado extends FormaGeometrica {
    private double lado;
    // ... construtor
    @Override
    public double calcularArea() {
        return lado * lado;
    }
}

public class Circulo extends FormaGeometrica {
    private double raio;
    // ... construtor
    @Override
    public double calcularArea() {
        return Math.PI * raio * raio;
    }
}

// Uso polimórfico
List<FormaGeometrica> formas = new ArrayList<>();
formas.add(new Quadrado(5));
formas.add(new Circulo(3));

for (FormaGeometrica forma : formas) {
    // Não precisamos saber se é um Quadrado ou Círculo!
    // A JVM decide qual método calcularArea() chamar em tempo de execução.
    System.out.println("Área: " + forma.calcularArea());
}
```

---

### 3.4. Abstração: Focando no Essencial

**O que é?**
É o processo de esconder os detalhes complexos de implementação e expor apenas a funcionalidade essencial para o usuário. A abstração foca no **"o que"** um objeto faz, em vez de **"como"** ele faz.

**Analogia:** Quando você dirige um carro, você interage com abstrações: volante, pedais, marcha. Você não precisa saber sobre a combustão do motor ou o sistema hidráulico dos freios. A complexidade está abstraída.

**Como em Java?**
Através de **classes abstratas** e **interfaces**.
*   **Classe Abstrata:** Uma classe que não pode ser instanciada. É um modelo para outras classes. Pode ter métodos abstratos (sem implementação) e métodos concretos (com implementação).
*   **Interface:** Um "contrato" 100% abstrato. Define um conjunto de métodos que uma classe deve implementar. Uma classe pode `implementar` várias interfaces.

**Por que é importante?**
*   **Simplificação:** Reduz a complexidade do sistema, permitindo que você se concentre em interações de alto nível.
*   **Desacoplamento:** Permite que as implementações mudem sem afetar as classes que dependem da abstração (da interface).

**Exemplo Prático (Interface):**

```java
// O Contrato: qualquer coisa que possa ser salva, deve ter este método.
public interface Armazenavel {
    void salvar();
    void carregar(int id);
}

// Duas implementações completamente diferentes do mesmo contrato.
public class UsuarioDAO implements Armazenavel {
    @Override
    public void salvar() {
        // Lógica para salvar o usuário em um banco de dados SQL...
    }
    // ...
}

public class ArquivoDeLog implements Armazenavel {
    @Override
    public void salvar() {
        // Lógica para escrever o log em um arquivo de texto...
    }
    // ...
}
```

---
**Recursos de Aprofundamento:**
*   **Vídeo:** [Pilares da POO - Código Fonte TV](https://www.youtube.com/watch?v=OE-H-21Sdp8)
*   **Artigo:** [Baeldung - Abstract Classes and Interfaces in Java](https://www.baeldung.com/java-abstract-class-interface)
*   **Discussão:** Tente pensar em um sistema (ex: um e-commerce) e identifique exemplos para cada pilar da OO. Onde você usaria herança? O que seria uma boa abstração? Compartilhe suas ideias. 