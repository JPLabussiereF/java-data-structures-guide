# Arrays e ArrayList

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

Arrays são estruturas de dados de tamanho fixo, enquanto ArrayList é uma implementação dinâmica baseada em arrays que cresce automaticamente.

## 🔍 Características

### Array Primitivo
- Tamanho fixo definido na criação
- Pode armazenar tipos primitivos e objetos
- Acesso direto à memória contígua
- Sem overhead de objetos wrapper

### ArrayList
- Tamanho dinâmico (cresce automaticamente)
- Apenas objetos (usa autoboxing para primitivos)
- Implementa interface List
- Capacidade inicial padrão de 10 elementos

## ⚖️ Trade-offs

### ✅ Vantagens

**Arrays:**
- Performance máxima para acesso aleatório: O(1)
- Menor uso de memória (sem overhead de ArrayList)
- Ideais para dados de tamanho fixo conhecido
- Suportam tipos primitivos diretamente
- Cache-friendly (localidade de memória)

**ArrayList:**
- Tamanho dinâmico e flexível
- Métodos úteis da API Collections
- Gerenciamento automático de capacidade
- Integração com streams e APIs modernas
- Facilita código limpo e manutenível

### ❌ Desvantagens

**Arrays:**
- Tamanho fixo (rígido)
- Inserções/remoções custosas: O(n)
- Sem métodos auxiliares built-in
- Gerenciamento manual de tamanho

**ArrayList:**
- Overhead de memória (objeto wrapper)
- Autoboxing/unboxing para primitivos (custo de performance)
- Redimensionamento ocasional causa cópia: O(n)
- Capacidade ociosa pode desperdiçar memória

## 📊 Complexidade (Big O)

| Operação | Array | ArrayList |
|----------|-------|-----------|
| Acesso por índice | O(1) | O(1) |
| Busca (não ordenado) | O(n) | O(n) |
| Inserção no final | O(1)* | O(1) amortizado** |
| Inserção no início | O(n) | O(n) |
| Inserção no meio | O(n) | O(n) |
| Remoção no final | O(1) | O(1) |
| Remoção no início | O(n) | O(n) |
| Remoção no meio | O(n) | O(n) |

*Apenas se houver espaço pré-alocado
**Pode ser O(n) quando precisa redimensionar

## 💡 Quando Usar

### Use Array quando:
- O tamanho é fixo e conhecido
- Performance crítica é necessária
- Trabalhar com grandes volumes de tipos primitivos
- Memória é limitada
- Operações são principalmente leitura

### Use ArrayList quando:
- Tamanho variável ou desconhecido
- Precisa de métodos convenientes da API
- Inserções/remoções no final são comuns
- Integração com Collections Framework
- Legibilidade do código é prioridade

## ⚠️ Quando Evitar

### Evite Array se:
- Tamanho muda frequentemente
- Necessita de muitas inserções/remoções
- Precisa de funcionalidades da API Collections

### Evite ArrayList se:
- Inserções/remoções frequentes no início/meio (use LinkedList)
- Trabalha com milhões de primitivos (use arrays)
- Memória é extremamente limitada
- Sincronização é necessária (use Vector ou Collections.synchronizedList)

## 💻 Exemplos Práticos

### Exemplo 1: Array Primitivo

```java
public class ArrayExemplo {
    public static void main(String[] args) {
        // Criação de array de tamanho fixo
        int[] numeros = new int[5];
        numeros[0] = 10;
        numeros[1] = 20;
        numeros[2] = 30;
        
        // Ou inicialização direta
        int[] valores = {1, 2, 3, 4, 5};
        
        // Acesso O(1)
        System.out.println("Primeiro: " + valores[0]); // 1
        
        // Iteração
        for (int i = 0; i < valores.length; i++) {
            System.out.println(valores[i]);
        }
        
        // Enhanced for
        for (int valor : valores) {
            System.out.println(valor);
        }
    }
}
```

### Exemplo 2: ArrayList Básico

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListExemplo {
    public static void main(String[] args) {
        // Criação com tipo genérico
        List<String> nomes = new ArrayList<>();
        
        // Adição O(1) amortizado
        nomes.add("Alice");
        nomes.add("Bob");
        nomes.add("Carlos");
        
        // Acesso O(1)
        System.out.println("Primeiro: " + nomes.get(0)); // Alice
        
        // Tamanho dinâmico
        System.out.println("Tamanho: " + nomes.size()); // 3
        
        // Inserção no meio O(n)
        nomes.add(1, "Diana"); // [Alice, Diana, Bob, Carlos]
        
        // Remoção O(n)
        nomes.remove("Bob"); // [Alice, Diana, Carlos]
        
        // Verificação
        if (nomes.contains("Alice")) {
            System.out.println("Alice está na lista");
        }
        
        // Iteração
        for (String nome : nomes) {
            System.out.println(nome);
        }
    }
}
```

### Exemplo 3: ArrayList com Capacidade Inicial

```java
import java.util.ArrayList;

public class ArrayListCapacidade {
    public static void main(String[] args) {
        // Evita redimensionamentos se você sabe o tamanho aproximado
        ArrayList<Integer> numeros = new ArrayList<>(1000);
        
        // Adicionar 1000 elementos não causará redimensionamento
        for (int i = 0; i < 1000; i++) {
            numeros.add(i); // O(1) garantido
        }
        
        // Capacidade vs Tamanho
        System.out.println("Tamanho: " + numeros.size()); // 1000
        // Capacidade é internal, não há getter público
        
        // TrimToSize reduz capacidade para tamanho atual
        numeros.trimToSize(); // Libera memória não utilizada
    }
}
```

### Exemplo 4: Comparação de Performance

```java
import java.util.ArrayList;

public class PerformanceComparacao {
    public static void main(String[] args) {
        int tamanho = 1_000_000;
        
        // Array primitivo - melhor performance
        long inicio = System.nanoTime();
        int[] arrayPrimitivo = new int[tamanho];
        for (int i = 0; i < tamanho; i++) {
            arrayPrimitivo[i] = i;
        }
        long tempoArray = System.nanoTime() - inicio;
        
        // ArrayList com Integer - boxing overhead
        inicio = System.nanoTime();
        ArrayList<Integer> arrayList = new ArrayList<>(tamanho);
        for (int i = 0; i < tamanho; i++) {
            arrayList.add(i); // autoboxing aqui
        }
        long tempoArrayList = System.nanoTime() - inicio;
        
        System.out.println("Array primitivo: " + tempoArray / 1_000_000 + " ms");
        System.out.println("ArrayList: " + tempoArrayList / 1_000_000 + " ms");
        // ArrayList é significativamente mais lento devido ao boxing
    }
}
```

### Exemplo 5: Conversão entre Array e ArrayList

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class ConversaoArrayArrayList {
    public static void main(String[] args) {
        // Array para ArrayList
        String[] arrayNomes = {"Alice", "Bob", "Carlos"};
        
        // Método 1: Arrays.asList (retorna lista de tamanho fixo!)
        List<String> lista1 = Arrays.asList(arrayNomes);
        // lista1.add("Diana"); // UnsupportedOperationException!
        
        // Método 2: Criar ArrayList mutável
        List<String> lista2 = new ArrayList<>(Arrays.asList(arrayNomes));
        lista2.add("Diana"); // OK
        
        // ArrayList para Array
        List<String> nomes = new ArrayList<>();
        nomes.add("Eva");
        nomes.add("Frank");
        
        // toArray com tipo específico
        String[] arrayResultado = nomes.toArray(new String[0]);
        // ou com tamanho pré-definido (mais eficiente)
        String[] arrayResultado2 = nomes.toArray(new String[nomes.size()]);
        
        System.out.println(Arrays.toString(arrayResultado));
    }
}
```

### Exemplo 6: ArrayList com Objetos Customizados

```java
import java.util.ArrayList;
import java.util.Comparator;

class Pessoa {
    String nome;
    int idade;
    
    Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }
    
    @Override
    public String toString() {
        return nome + " (" + idade + ")";
    }
}

public class ArrayListObjetos {
    public static void main(String[] args) {
        ArrayList<Pessoa> pessoas = new ArrayList<>();
        
        pessoas.add(new Pessoa("Alice", 30));
        pessoas.add(new Pessoa("Bob", 25));
        pessoas.add(new Pessoa("Carlos", 35));
        
        // Busca personalizada O(n)
        for (Pessoa p : pessoas) {
            if (p.nome.equals("Bob")) {
                System.out.println("Encontrado: " + p);
            }
        }
        
        // Ordenação O(n log n)
        pessoas.sort(Comparator.comparingInt(p -> p.idade));
        System.out.println("Ordenado por idade: " + pessoas);
        
        // Streams (Java 8+)
        pessoas.stream()
            .filter(p -> p.idade > 28)
            .forEach(System.out::println);
    }
}
```

### Exemplo 7: Problemas Comuns e Soluções

```java
import java.util.ArrayList;
import java.util.Iterator;

public class ProblemasComuns {
    public static void main(String[] args) {
        ArrayList<String> lista = new ArrayList<>();
        lista.add("A");
        lista.add("B");
        lista.add("C");
        lista.add("B");
        lista.add("D");
        
        // PROBLEMA 1: ConcurrentModificationException
        // ERRADO:
        // for (String item : lista) {
        //     if (item.equals("B")) {
        //         lista.remove(item); // Exception!
        //     }
        // }
        
        // CORRETO: Use Iterator
        Iterator<String> iter = lista.iterator();
        while (iter.hasNext()) {
            String item = iter.next();
            if (item.equals("B")) {
                iter.remove(); // OK
            }
        }
        
        // Ou use removeIf (Java 8+)
        lista.add("B");
        lista.removeIf(item -> item.equals("B")); // Melhor solução
        
        System.out.println(lista); // [A, C, D]
        
        // PROBLEMA 2: Performance em loop reverso
        // ERRADO (para remoções):
        lista = new ArrayList<>();
        lista.add("A");
        lista.add("B");
        lista.add("C");
        
        // Remover do início é O(n) por elemento = O(n²) total
        for (int i = 0; i < lista.size(); i++) {
            lista.remove(0); // Muito lento!
        }
        
        // CORRETO: Remova do final para trás
        lista = new ArrayList<>();
        lista.add("A");
        lista.add("B");
        lista.add("C");
        
        for (int i = lista.size() - 1; i >= 0; i--) {
            lista.remove(i); // O(1) por elemento = O(n) total
        }
    }
}
```

## 🎯 Dicas de Performance

1. **Pré-aloque capacidade**: Se conhece o tamanho, use `new ArrayList<>(tamanho)`
2. **Use array para primitivos**: Evite boxing/unboxing desnecessário
3. **Remova do final**: Operações no final são O(1)
4. **Evite `ensureCapacity`**: Se já alocou capacidade inicial adequada
5. **Use `trimToSize`**: Para liberar memória não utilizada após carregamento

## 🔗 Relacionados

- [LinkedList](./linkedlist.md) - Alternativa para inserções/remoções frequentes
- [Comparação Geral](./comparacao-geral.md) - Comparação de todas as estruturas

---

[← Voltar ao Índice](../README.md)
