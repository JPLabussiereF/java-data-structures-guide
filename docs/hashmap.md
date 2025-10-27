# HashMap

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

HashMap é a implementação mais usada de Map em Java, oferecendo acesso rápido por chave através de hashing.

## 🔍 Características

- Baseado em hash table com buckets
- Não mantém ordem
- Permite uma chave null e múltiplos valores null
- Não é thread-safe
- Capacidade inicial padrão: 16, load factor: 0.75

## ⚖️ Trade-offs

### ✅ Vantagens
- **Operações O(1) em média** para get/put/remove
- Muito rápido para lookup por chave
- Flexível e versátil
- Baixo overhead quando bem dimensionado

### ❌ Desvantagens
- Sem ordem garantida
- Performance degrada com colisões
- Requer boa implementação de hashCode/equals
- Redimensionamento custoso

## 📊 Complexidade

| Operação | Média | Pior Caso |
|----------|-------|-----------|
| get | O(1) | O(n) |
| put | O(1) | O(n) |
| remove | O(1) | O(n) |
| containsKey | O(1) | O(n) |

## 💻 Exemplos

```java
import java.util.*;

public class HashMapExemplo {
    public static void main(String[] args) {
        Map<String, Integer> idades = new HashMap<>();
        
        // Put O(1)
        idades.put("Alice", 30);
        idades.put("Bob", 25);
        idades.put("Carlos", 35);
        
        // Get O(1)
        System.out.println("Idade de Bob: " + idades.get("Bob")); // 25
        
        // ContainsKey O(1)
        if (idades.containsKey("Alice")) {
            System.out.println("Alice encontrada");
        }
        
        // Iterar
        for (Map.Entry<String, Integer> entry : idades.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
        
        // GetOrDefault
        int idadeDefault = idades.getOrDefault("Diana", 0);
        System.out.println("Idade de Diana: " + idadeDefault); // 0
        
        // PutIfAbsent
        idades.putIfAbsent("Alice", 40); // Não sobrescreve
        System.out.println("Alice: " + idades.get("Alice")); // 30
        
        // Compute
        idades.compute("Bob", (k, v) -> v + 1); // Bob agora tem 26
        
        // Merge
        idades.merge("Carlos", 5, Integer::sum); // Carlos: 35 + 5 = 40
    }
}
```

### Exemplo: Contagem de Frequência

```java
import java.util.*;

public class ContagemFrequencia {
    public static Map<Character, Integer> contarCaracteres(String texto) {
        Map<Character, Integer> frequencia = new HashMap<>();
        
        for (char c : texto.toCharArray()) {
            frequencia.put(c, frequencia.getOrDefault(c, 0) + 1);
            // Ou: frequencia.merge(c, 1, Integer::sum);
        }
        
        return frequencia;
    }
    
    public static void main(String[] args) {
        String texto = "hello world";
        Map<Character, Integer> freq = contarCaracteres(texto);
        
        System.out.println(freq);
        // {h=1, e=1, l=3, o=2, w=1, r=1, d=1, ...}
    }
}
```

## 🎯 Quando Usar

- Lookup rápido por chave
- Cache de objetos
- Contagem/frequência
- Índice/dicionário
- Quando ordem não importa

---

[← Voltar ao Índice](../README.md)
