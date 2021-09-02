# Taller Pre Básicos \#1

## Plantilla estándar

```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    // Code ...
    return 0;
}
```
## Variables

### Integers

- Representan enteros desde $-2^{31}$ hasta $2^{31}-1$.
- Esto es, aproximadamente desde $-2\times 10^{9}$ hasta $2 \times 10^{9}$.
- Uso de memoria: 4 bytes.

```cpp
int a; //Válido
int 123a; //No válido
int q1, q2, _, _113 //Válido
```
### Leyendo variables

```cpp
int a;
cin >> a;
```

```cpp
int a, b;
cin >> a >> b;
```

```cpp
int a, b;
cin >> a;
cin >> b;
```

### Suma de dos variables

```cpp
int a = 2, b = 4;
int c = a + b;
```

### Operaciones

```cpp
a+b; // Suma de a y b.
a*b; // Multiplicación de a y b
a/b; // División (int) de a y b
a%b; // Módulo (o residuo) de a en b
```

### Impriminedo valores

```cpp
cout << 2; //Imprime '2' 
cout << 2 << 3 << 4; //Imprime '234'
cout << 2 << " " << 3 << " " << 4; //Imprime '2 3 4'
cout << "Hello World!"; //Imprime 'Hello World!'
cout << 2 << endl << 3; //Imprime '2
                        //         3'
```

### Ejemplo

Lea dos números enteros $a$ y $b$ e imprima la suma.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int a, b;
    cin >> a >> b;
    int c = a + b;
    cout << c << endl;
    return 0;
}
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int a, b;
    cin >> a >> b;
    cout << a + b << endl;
    return 0;
}
```
