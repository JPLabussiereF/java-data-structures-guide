# ConcurrentHashMap

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

ConcurrentHashMap é uma implementação thread-safe e de alta performance de Map, usando lock striping.

## 🔍 Características

- Thread-safe sem lock global
- Lock striping (múltiplos locks por segmentos)
- NÃO permite null key nem null value
- Operações atômicas built-in
- Melhor alternativa a Hashtable

## ⚖️ Trade-offs

### ✅ Vantagens
- **Altíssima concorrência** (múltiplas threads simultâneas)
- Sem lock global (apenas segmentos)
- Operações atômicas (putIfAbsent, compute, etc)
- Performance superior ao Hashtable
- Reads geralmente sem lock

### ❌ Desvantagens
- Não permite null
- Overhead maior que HashMap (locks)
- Iteradores weakly consistent
- Tamanho pode ser impreciso durante updates

## 📊 Complexidade

| Operação | Complexidade |
|----------|--------------|
| get | O(1) - sem lock* |
| put | O(1) - lock apenas no segmento |
| remove | O(1) - lock apenas no segmento |

*Reads geralmente não bloqueiam

## 💻 Exemplos

### Exemplo 1: Uso Básico

```java
import java.util.concurrent.ConcurrentHashMap;

public class ConcurrentHashMapExemplo {
    public static void main(String[] args) {
        ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
        
        // Thread-safe
        map.put("A", 1);
        map.put("B", 2);
        
        // Operações atômicas
        map.putIfAbsent("A", 10); // Não sobrescreve
        System.out.println(map.get("A")); // 1
        
        // Compute atomicamente
        map.compute("C", (k, v) -> v == null ? 1 : v + 1);
        System.out.println(map.get("C")); // 1
        
        map.compute("C", (k, v) -> v + 1);
        System.out.println(map.get("C")); // 2
    }
}
```

### Exemplo 2: Contador Concorrente

```java
import java.util.concurrent.*;

public class ContadorConcorrente {
    private ConcurrentHashMap<String, Integer> contador = new ConcurrentHashMap<>();
    
    public void incrementar(String chave) {
        // Atômico e thread-safe
        contador.merge(chave, 1, Integer::sum);
    }
    
    public int getContador(String chave) {
        return contador.getOrDefault(chave, 0);
    }
    
    public static void main(String[] args) throws InterruptedException {
        ContadorConcorrente cont = new ContadorConcorrente();
        
        // Múltiplas threads incrementando
        ExecutorService executor = Executors.newFixedThreadPool(10);
        
        for (int i = 0; i < 1000; i++) {
            executor.submit(() -> cont.incrementar("clicks"));
        }
        
        executor.shutdown();
        executor.awaitTermination(1, TimeUnit.MINUTES);
        
        System.out.println("Total clicks: " + cont.getContador("clicks"));
        // 1000 - sem race condition!
    }
}
```

### Exemplo 3: Cache Thread-Safe

```java
import java.util.concurrent.ConcurrentHashMap;

public class CacheThreadSafe<K, V> {
    private final ConcurrentHashMap<K, V> cache = new ConcurrentHashMap<>();
    
    public V getOrCompute(K key, Function<K, V> computador) {
        return cache.computeIfAbsent(key, computador);
    }
    
    public void invalidar(K key) {
        cache.remove(key);
    }
    
    public static void main(String[] args) {
        CacheThreadSafe<Integer, String> cache = new CacheThreadSafe<>();
        
        // Múltiplas threads podem chamar isso simultaneamente
        String valor = cache.getOrCompute(1, id -> {
            // Simula cálculo pesado
            return "Valor para " + id;
        });
        
        System.out.println(valor);
    }
}
```

## 🎯 Quando Usar

- Aplicações multi-thread
- Cache compartilhado entre threads
- Substituir Hashtable
- Alta concorrência de leitura e escrita

## 🔗 Relacionados
- [HashMap](./hashmap.md) - Versão single-thread
- [Hashtable](./hashtable.md) - Versão legada (evite)

---

[← Voltar ao Índice](../README.md)
