# LinkedHashMap

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

LinkedHashMap é um HashMap que mantém ordem de inserção (ou acesso) através de lista encadeada.

## 🔍 Características

- Baseado em HashMap + lista duplamente encadeada
- Mantém ordem de inserção OU ordem de acesso
- Permite null key e null values
- Ideal para implementar LRU cache

## ⚖️ Trade-offs

### ✅ Vantagens
- Mantém ordem previsível
- Operações O(1) em média
- Pode usar ordem de acesso para LRU
- Iteração eficiente em ordem

### ❌ Desvantagens
- Maior uso de memória
- Ligeiramente mais lento que HashMap

## 📊 Complexidade

Mesma do HashMap: O(1) médio para operações principais

## 💻 Exemplo: LRU Cache

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacidade;
    
    public LRUCache(int capacidade) {
        super(capacidade, 0.75f, true); // true = ordem de acesso
        this.capacidade = capacidade;
    }
    
    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacidade;
    }
    
    public static void main(String[] args) {
        LRUCache<Integer, String> cache = new LRUCache<>(3);
        
        cache.put(1, "A");
        cache.put(2, "B");
        cache.put(3, "C");
        
        cache.get(1); // Acessa A (move para final)
        
        cache.put(4, "D"); // Remove B (menos usado recentemente)
        
        System.out.println(cache); // {3=C, 1=A, 4=D}
    }
}
```

---

[← Voltar ao Índice](../README.md)
