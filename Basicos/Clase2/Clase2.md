![xd](https://i.ytimg.com/vi/47GRtdHOKMg/maxresdefault.jpg)

Una forma de aproximar el tiempo que toma nuestro código en ejecutarse es contando la cantidad de operaciones *básicas* que realiza.

Se consideran operaciones básicas:

- Operaciones aritméticas (+, -, *, /, %, <, >, =)
- Operaciones lógicas (or, and, not, xor)
- Acceder al valor de un array
- Definir una nueva variable

¿Cuáles no son operaciones básicas?:

- Comparar strings, vectores
- Definir un vector
- Concatenar 2 strings

```c++
#include <bits/stdc++.h>
using namespace std;

void f(int x){
    int ans = 0;
    for(int i=0; i<x; i++) ans += i;
}

int main(){
    int n; cin >> n;
    for(int i=0; i<n; i++){
        f(10);
    }
    for(int i=0; i<n; i++){
        f(i);
    }
}
```

Consideramos que una computadora puede realizar hasta $10^8$ operaciones básicas por segundo. Entonces, calcular el tiempo de ejecución sería:

$$
\text{tiempo} = \frac{\text{\# operaciones}}{10^8}
$$

Una forma más efectiva de medir esto, es con la complejidad asintótica del código.

![xd](https://www.vegait.rs/media/4767/comparisonx2.png?width=350&height=350)

# Complejidad asintótica

- El objetivo es resolver los problemas rápido
- Probar en el peor escenario posible
- Medir tiempos rápidamente
- Predecir el tiempo antes de implementarlo
- Hacer soluciones rápidas

```c++
for(int i=0; i<n; i++){ // O(n)
    for(int j=0; j<m; j++){ // O(m)
        ...
        doSomething();
        ...
    } // O(m)*O(doSomething)
}// O(n)*O(m)*O(doSomething)
```


```c++
void f(int x){
    int ans = 0; // O(1)
    for(int i=0; i<x; i++){
        ans += i; // O(1)
    } // O(x)
}// O(x) + O(1) = O(x)

for(int i=0; i<n; i++){
    f(10); // O(10)
}// O(10*n) = O(n)

for(int i=0; i<n; i++){
    f(i); // O(i)
} // Sum_{i=0}^{n} O(i) = 
// O(1) + O(2) + ... + O(n-1) + O(n) = O(n^2)
```
Así, si $ n = 10^5 $:

```c++
void f(int x){
    int ans = 0; // O(1)
    for(int i=0; i<x; i++){
        ans += i; // O(1)
    } // O(x)
}// O(x) -> t = 10^5/10^8 = 0.001 s 

for(int i=0; i<n; i++){
    f(10); // O(10)
}// O(10*n) = O(n) -> t = 10^5/10^8 = 0.001 s

for(int i=0; i<n; i++){
    f(i); // O(i)
} // Sum_{i=0}^{n} O(i) = 
// O(1) + O(2) + ... + O(n-1) + O(n) = O(n^2)
// t = (10^5)^2/10^8 = 10^2 s
```

Un algoritmo tiene complejidad asintótica $O(f(n))$ si este no realiza más que $C \cdot f(n)$ operaciones en cualquier input, donde $C$ es algún número constante.

## Operaciones

| *Ligero* | *Pesado* |
|---------|----------|
|+, -| % |
|* | Insertar elementos |
|Logicas | Input/Output |

## Planeando una solución

- Tu solución es lenta
- Primero, intenta mejorarla asintóticamente
- Reduce la complejidad en operaciones costosas
- Si aún tienes TLE, mejora tus constantes. Solo si estás cerca de las $10^8$ operaciones
- Evita operaciones pesadas

## Ejemplos

### Substring problem

Dados dos strings $s$ y $t$, verificar si $s$ es un substring de $t$.


| *Input* | *Output* |
|---------|----------|
|abac abacabad| Yes |
|cac abacabad | No |
|abab abacabab | Yes |

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
    string s, t; // O(1)
    cin >> s >> t; // O(|t| + |s|)
    int sz = s.size(); // O(1)
    for(int i=0; i<t.size()-sz+1; i++){ // O(|t|)
        bool test = true; // O(1)
        for(int j=0; j<sz; j++){ // O(|s|)
            if(s[j] != t[i+j]) test = false; // O(1)
        } // O(|s|)
        if(test){
            cout << "Yes";
            return 0;
        } // O(1)
    } // O(|t|*|s|)
    cout << "No";
    return 0;
}
```


### Mathemagics

```c++
void f(int n){
    vector <bool> a(n, true);
    for(int i=2; i<n; i++){
        for(int j=i; j<n; j+=i) a[j] = false;
    }
}
```

```c++
void f(int n){
    vector <bool> a(n, true);
    for(int i=2; i<n; i++){
        if(a[i]){
            //cout << i << " ";
            for(int j=i; j<n; j+=i) a[j] = false;
        }
    }
}
```

### Little Pony and Sort by Shift

Dado un array de $n$ elementos. Calcular el mínimo número de operaciones que se necesita para ordenarlo, siendo la operación permitida mover el último elemento al inicio de la secuencia.

***Input***

The first line contains an integer $n$ $(2 \leq n \leq 10^5)$. The second line contains $n$ integer numbers $a_1, a_2, \ldots, a_n$ $(1 \leq a_{i} \leq 10^5)$.

***Output***

If it's impossible to sort the sequence output -1. Otherwise output the minimum number of operations.

```c++
#include <bits/stdc++.h>
using namespace std;

int n;
int getPos(int arr[]){
    int p = -1;
    for(int i=0; i<n-1; i++){
    	if(arr[i] > arr[i+1]){
        	if(p == -1) p = i;
        	else return -1;
    	}
    }
    if(p == -1) p = n-1;
    return p;
}

int solve(int arr[]){
    int p = getPos(arr);
    if(p == -1) return -1;
    if(p == n-1) return 0;
    if(arr[0] >= arr[n-1]) return n-p-1;
    else return -1;
}

int main(){
    cin >> n;
    int arr[n];
    for(int i=0; i<n; i++) cin >> arr[i];
    int ans = solve(arr);
    cout << ans;
    return 0;
}
```

### The Monster

A monster is chasing after Rick and Morty on another planet. They're so frightened that sometimes they scream. More accurately, Rick screams at times $b, b + a, b + 2a, b + 3a, \ldots$ and Morty screams at times $d, d + c, d + 2c, d + 3c, \ldots$

The Monster will catch them if at any point they scream at the same time, so it wants to know when it will catch them (the first time they scream at the same time) or that they will never scream at the same time.

***Input***

The first line of input contains two integers $a$ and $b$ $(1 \leq a, b \leq 100)$.

The second line contains two integers $c$ and $d$ $(1 \leq c, d \leq 100)$.

***Output***

Print the first time Rick and Morty will scream at the same time, or  - 1 if they will never scream at the same time.

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int a, b, c, d; cin >> a >> b >> c >> d;
	for(int i=0; i<=100; i++){
		int aux = d+c*i;
		int k = (aux-b)/a;
		if((aux-b)%a == 0 && k >= 0){
			cout << aux << '\n';
			return 0;
		}
	}
	cout << -1;
    return 0;
}
```

$$
b + ka = d + pc
$$

$$
ka = (d-b)+pc \qquad\qquad g = \gcd(a, d-b)
$$

$$
k\frac{a}{g} = \frac{d-b}{g} + \frac{pc}{g}
$$

$$
pc \equiv 0 \mod g
$$

$$
p \equiv 0 \mod \frac{g}{\gcd (c, g)}
$$

```c++
#include <bits/stdc++.h>
using namespace std;
int main(){
	int a, b, c, d; cin >> a >> b >> c >> d;
	if(d < b){
		swap(d, b);
		swap(c, a);
	}
	int g = __gcd(a, d-b);
	int m_p = g/__gcd(c, g);
	for(int i=0; i<=(100)/m_p; i++){
		int aux = d+c*i*m_p;
		int k = (aux-b)/a;
		if((aux-b)%a == 0 && k >= 0){
			cout << aux << '\n';
			return 0;
		}
	}
	cout << -1;
	return 0;
}
```

$$
g = \gcd(a, d-b) \quad\quad x = \frac{a}{g} \quad\quad y = \frac{d-b}{g}
$$

$$
G = \gcd(c, g) \quad\quad u = \frac{c}{G} \quad\quad v = \frac{g}{G}
$$

$$
p \equiv 0 \mod v
$$

$$
\frac{p}{v} u \equiv -y \mod x
$$

$$
\frac{p}{v} \equiv \frac{-y}{\gcd(u, x)}\Bigg(\phi\left(\frac{u}{\gcd(u, x)}\right)\Bigg)^{-1} \mod x
$$

$$
p = v\Bigg(\frac{-y}{\gcd(u, x)}\Bigg(\phi\left(\frac{u}{\gcd(u, x)}\right)\Bigg)^{-1} + xJ\Bigg)
$$

$$
t = \min(pc + d) = \min(p)c + d
$$

```c++
#include <bits/stdc++.h>
using namespace std;

int fastexp(int x, int y, int p){
	int ans = 1;
	while(y > 0){
		if(y&1) ans = (ans*x)%p;
		y = y>>1;
		x = (x*x)%p;
	}
	return ans%p;
}

int phi(int x){
	int ans = x;
	for(int i=2; i*i<=x; i++){
		if(x%i == 0){
			ans *= (i-1);
			ans /= i;
			while(x%i == 0) x /= i;
		}
	}
	if(x != 1){
		ans *= (x-1);
		ans /= x;
	}
	return ans;
}

int main(){
	int a, b, c, d; 
    cin >> a >> b >> c >> d;
	if(d < b){
		swap(d, b);
		swap(c, a);
	}
	int g = __gcd(a, d-b);
	int G = __gcd(c, g);
	int u = c/G;
	int v = g/G;
	int x = a/g;
	int y = (d-b)/g;
	int m = __gcd(x, u);
	if(y%m == 0){
		int k = (-fastexp(u/m, phi(x)-1,x)*(y/m))%x;
		if(k < 0) k += x;
		cout << k*v*c+d << '\n';
	}
	else cout << -1 << '\n';
	return 0;
}
```