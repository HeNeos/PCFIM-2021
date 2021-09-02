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
#### Leyendo variables

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

#### Suma de dos variables

```cpp
int a = 2, b = 4;
int c = a + b;
```

#### Operaciones

```cpp
a+b; // Suma de a y b.
a*b; // Multiplicación de a y b
a/b; // División (int) de a y b
a%b; // Módulo (o residuo) de a en b
```

#### Impriminedo valores

```cpp
cout << 2; //Imprime '2' 
cout << 2 << 3 << 4; //Imprime '234'
cout << 2 << " " << 3 << " " << 4; //Imprime '2 3 4'
cout << "Hello World!"; //Imprime 'Hello World!'
cout << 2 << endl << 3; //Imprime '2
                        //         3'
```

#### Ejemplo

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

### Long long integers

- Representan enteros desde $-2^{63}$ hasta $2^{63}-1$.
- Esto es, aproximadamente desde $-9\times 10^{18}$ hasta $9 \times 10^{18}$.
- Uso de memoria: 8 bytes.

#### Cuándo usar long long en vez de int

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int a = 1000000*1000000;
    cout << a << endl; // Imprime -727379968
    return 0;
}
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    long long a = 1000000LL*1000000LL;
    cout << a << endl; // Imprime 10^12
    return 0;
}
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int a;
    cin >> a; // Input: 10^6
    cout << a*a << endl; // Imprime -727379968
    return 0;
}
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    long long a;
    cin >> a; // Input: 10^6
    cout << a*a << endl; // Imprime 10^12
    return 0;
}
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int a = 2147483647;
    a = a+1;
    cout << a << endl; // Imprime -2147483648
    return 0;
}
```

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    long long a = 2147483647;
    a = a+1;
    cout << a << endl; // Imprime 2147483648
    return 0;
}
```