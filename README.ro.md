*[English](README.md) · **Română***

# Exerciții Java — Anul II

Un mic repository de lucru de la cursul de Java din anul al doilea. Conține un singur exercițiu
algoritmic complet, **problema celor opt regine**, rezolvată prin backtracking.

| | |
|---|---|
| **Autor** | Ștefan Horia-Eusebiu |
| **Limbaj** | Java 17 (proiect Maven, fără dependențe externe) |
| **An** | 2024 |

## Problema celor opt regine

[`OptRegine.java`](src/main/java/javaAn2/OptRegine.java) așază opt regine pe o tablă de șah astfel
încât niciuna să nu o atace pe alta. Tabla este o matrice `int[8][8]`, iar căutarea avansează
**coloană cu coloană**:

```java
private boolean plaseazaRegine(int[][] tabla, int coloana) {
    if (coloana >= N) return true;              // toate coloanele completate → soluție găsită
    for (int i = 0; i < N; i++) {
        if (esteSigur(tabla, i, coloana)) {
            tabla[i][coloana] = 1;              // plasare
            if (plaseazaRegine(tabla, coloana + 1)) return true;
            tabla[i][coloana] = 0;              // backtrack
        }
    }
    return false;
}
```

Pentru că pe fiecare coloană se plasează exact o regină, `esteSigur()` trebuie să verifice doar trei
direcții spre stânga: linia, diagonala stânga-sus și diagonala stânga-jos. Tot ce e în dreapta este
încă gol, deci nu trebuie verificat deloc. Datorită acestei observații, testul de siguranță rămâne
`O(n)` în loc de `O(n²)`.

Soluția este afișată ca o tablă text, cu `R` pentru regină și `.` pentru pătrat gol.

> Problemă cunoscută: în `afiseazaTabla()`, o regină se afișează ca `"R"`, iar un pătrat gol ca `". "`,
> așa că coloanele nu se aliniază. Afișarea `"R "` rezolvă alinierea.

## Rulare

```bash
mvn compile
mvn exec:java -Dexec.mainClass="javaAn2.OptRegine"
```

Sau deschide proiectul în IntelliJ IDEA și rulează direct `OptRegine`.

`Main.java` este clasa implicită generată de IDE și afișează doar un salut urmat de numerele de la
1 la 5; nu face parte din exercițiu.

---

Lucrare academică publicată în scop de portofoliu.
