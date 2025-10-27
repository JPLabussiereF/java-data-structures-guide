# Hashtable

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

Hashtable é uma implementação legada e sincronizada de Map. **Evite usar em código novo - use HashMap ou ConcurrentHashMap.**

## 🔍 Características

- Classe legada (desde Java 1.0)
- Thread-safe (sincronizado)
- NÃO permite null key nem null value
- Sincronização em todos os métodos

## ⚖️ Trade-offs

### ✅ Vantagens
- Thread-safe out-of-the-box
- Simples para concorrência básica

### ❌ Desvantagens
- **Obsoleto** - não use em código novo
- Sincronização global (lock em toda tabela)
- Performance muito inferior ao ConcurrentHashMap
- API desatualizada
- Bloqueio excessivo

## 📊 Complexidade

Mesma do HashMap: O(1) médio, mas COM overhead de sincronização

## 💻 Exemplo (NÃO RECOMENDADO)

```java
import java.util.Hashtable;

public class HashtableExemplo {
    public static void main(String[] args) {
        // NÃO USE ISSO - apenas para referência
        Hashtable<String, Integer> tabela = new Hashtable<>();
        
        tabela.put("A", 1);
        // tabela.put(null, 2); // NullPointerException!
        
        System.out.println(tabela.get("A"));
    }
}
```

## ⚠️ Use Ao Invés

```java
// Para código não-concorrente:
Map<String, Integer> map = new HashMap<>();

// Para código concorrente:
Map<String, Integer> map = new ConcurrentHashMap<>();

// Para sincronização simples:
Map<String, Integer> map = Collections.synchronizedMap(new HashMap<>());
```

## 🎯 Quando NÃO Usar

**NUNCA use Hashtable em código novo. Use:**
- `HashMap` para single-thread
- `ConcurrentHashMap` para multi-thread
- `Collections.synchronizedMap()` se precisa de sincronização total

---

[← Voltar ao Índice](../README.md)
