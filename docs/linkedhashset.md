# LinkedHashSet

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

LinkedHashSet é um HashSet que mantém a ordem de inserção dos elementos através de uma lista duplamente encadeada.

## 🔍 Características

- Baseado em LinkedHashMap
- Mantém ordem de inserção
- Não permite duplicatas
- Permite um elemento null
- Overhead de memória maior que HashSet

## ⚖️ Trade-offs

### ✅ Vantagens
- Mantém ordem de inserção (previsível)
- Operações O(1) em média
- Iteração ordenada
- Combina velocidade do HashSet com ordem

### ❌ Desvantagens
- Maior uso de memória (lista encadeada)
- Ligeiramente mais lento que HashSet
- Mais complexo internamente

## 📊 Complexidade

| Operação | Complexidade |
|----------|--------------|
| add | O(1) |
| remove | O(1) |
| contains | O(1) |
| Iteração | O(n) - em ordem! |

## 💻 Exemplo

```java
import java.util.LinkedHashSet;
import java.util.Set;

public class LinkedHashSetExemplo {
    public static void main(String[] args) {
        Set<String> frutas = new LinkedHashSet<>();
        
        frutas.add("Maçã");
        frutas.add("Banana");
        frutas.add("Laranja");
        frutas.add("Banana"); // Duplicata ignorada
        
        // Iteração mantém ordem de inserção
        for (String fruta : frutas) {
            System.out.println(fruta);
        }
        // Output: Maçã, Banana, Laranja (nessa ordem!)
    }
}
```

## 🎯 Quando Usar

- Precisa eliminar duplicatas MAS manter ordem
- Cache com ordem de inserção
- Histórico sem duplicatas

---

[← Voltar ao Índice](../README.md)
