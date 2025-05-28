Claro! Abaixo está o algoritmo **Bubble Sort** em **pseudocódigo** e em **Python**, com explicação detalhada de seu funcionamento.

---

## 📌 O que é o Bubble Sort?

O **Bubble Sort** é um algoritmo de ordenação simples que percorre repetidamente a lista, compara elementos adjacentes e os troca de lugar se estiverem na ordem errada. Esse processo é repetido até que a lista esteja ordenada.

---

## 🧠 Funcionamento Detalhado

1. Percorre o vetor da esquerda para a direita.
2. Compara dois elementos adjacentes.
3. Se o da esquerda for maior que o da direita, troca-os de lugar.
4. Após cada passagem completa, o maior elemento "borbulha" para o final da lista.
5. O processo se repete, ignorando a última posição já ordenada, até que nenhuma troca seja necessária.

---

## 🔢 Pseudocódigo

```plaintext
Algoritmo BubbleSort
Entrada: Lista A com n elementos

Para i de 0 até n - 1 faça
    Para j de 0 até n - i - 2 faça
        Se A[j] > A[j + 1] então
            Trocar A[j] com A[j + 1]
        FimSe
    FimPara
FimPara

Retornar A ordenado
```

---

## 🐍 Código em Python

```python
def bubble_sort(lista):
    n = len(lista)

    # Loop externo para cada elemento da lista
    for i in range(n):
        # Flag para indicar se houve troca nesta passada
        trocou = False

        # Loop interno para comparar elementos adjacentes
        for j in range(0, n - i - 1):
            if lista[j] > lista[j + 1]:
                # Troca os elementos
                lista[j], lista[j + 1] = lista[j + 1], lista[j]
                trocou = True
        
        # Se não houve troca, a lista já está ordenada
        if not trocou:
            break

    return lista

# Exemplo de uso
valores = [5, 2, 9, 1, 5, 6]
print("Lista ordenada:", bubble_sort(valores))
```

---

## 🧪 Exemplo de Execução

Para a lista `[5, 2, 9, 1]`:

1ª Passada:

* Compara 5 e 2 → troca → `[2, 5, 9, 1]`
* Compara 5 e 9 → ok
* Compara 9 e 1 → troca → `[2, 5, 1, 9]`

2ª Passada:

* Compara 2 e 5 → ok
* Compara 5 e 1 → troca → `[2, 1, 5, 9]`

3ª Passada:

* Compara 2 e 1 → troca → `[1, 2, 5, 9]`

4ª Passada:

* Nenhuma troca → ordenado → encerra.

---

## ✅ Vantagens e Desvantagens

**Vantagens**:

* Simples de entender e implementar.
* Bom para listas pequenas.

**Desvantagens**:

* Ineficiente para grandes volumes (complexidade O(n²)).
* Muitas comparações e trocas.

---

