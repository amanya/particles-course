# Explosió de partícules

Explicació pas a pas de com programar una explosió de partícules fent servir el
llenguatge de programació C.

## Pas 1: Dibuixem en una finestra!

Posa el codi següent en un arxiu anomenat `particles.c`:

```c
#include <raylib.h>

#define SCREEN_WIDTH 1200
#define SCREEN_HEIGHT 800

int main(int argc, char *argv[]) {
    InitWindow(SCREEN_WIDTH, SCREEN_HEIGHT, "Explosió de partícules");

    while(!WindowShouldClose()) {
        BeginDrawing();
        ClearBackground(BLACK);
        DrawRectangle(100, 100, 10, 10, WHITE);
        EndDrawing();
    }

    CloseWindow();
    return 0;
}
```

A la primera línia veiem que "incloem" una llibreria anomenada [raylib](https://www.raylib.com/index.html). El creador de Raylib la defineix com *una llibreria senzilla i fàcil de fer servir per gaudir programant videojocs*. Si tens una estona et pots entretenir mirant [els exemples](https://www.raylib.com/examples.html) o [aquesta xuleta](https://www.raylib.com/cheatsheet/cheatsheet.html) amb totes les funcions.

Com que raylib és una llibreria que no pertany a l'especificació del llenguatge C, abans de fer-la servir, ens hem d'assegurar que la tenim correctament instal·lada. Demana a un adult que t'ajudi a fer-ho si és necessari.

A més a més, li haurem d'indicar al compilador on pot trobar raylib. Perque no ho haguem d'escriure cada vegada, posarem la comanda per cridar al compilador en un *shell script*, un petit programa que executarem cada vegada que volguem compilar el codi.

Posa el codi següent en un arxiu anomenat `build.sh`:

```
#!/bin/sh

cc particles.c -g $(pkg-config --libs --cflags raylib) -o particles
```

Finalment, haurem d'indicar al sistema operatiu que `build.sh` és un programa que podem executar. Per fer-ho utilitzem la següent comanda:

```sh
$ chmod +x build.sh
```

A partir d'ara, sempre que volem compilar el nostre programa, simplement haurem d'executar la comanda següent:

```sh
$ ./build.sh
```

> [!NOTE]
> Si et preguntes per què hem de posar `./` davant del nostre executable, la raó és senzilla però potser no evident. El punt `.` és un sinònim del "directori actual", per tant estem dient que executi `build.sh` dins del directori actual. El sistema operatiu ens obliga a ser explícit quan volem executar algúna cosa del directory actual per protegir-nos: imagina't què passaria si algú posés un programa maliciós anomenat de la mateixa manera que una comanda inofensiva del sistema operatiu, `ls` per exemple, podria enganyar-nos molt fàcilment.

Si la compilació ha anat bé, veurem que tenim un executable anomenat `particles` al nostre directori actual. Com l'hem d'executar? Exacte, indicant el directori actual amb el `.`:

```sh
$ ./particles
```

Si tot ha anat bé, hauríes de veure una finestra negra amb un quadradet blanc petit al mig. Un cop hagis acabat d'admirar-la, pots tancar-la apretant `Esc` o amb el botó de tancar.

### Hora de jugar!

No cal que entenguis totes les línies del programes que acabes d'escriure però si que et pot anar bé tocar algunes coses, jugar i experimentar amb diferents valors per veure què passa. A continuació t'explicaré algunes coses interessants del codi.

1. Prova de canviar les mides de la finestra donant uns valors diferents a `SCREEN_WIDTH` i `SCREEN_HEIGHT`.

2. El codi entra en un bucle que no s'acaba fins que la funció `WindowShouldClose` retorna true. Això passa, per exemple, quan apretes la tecla `Esc`. El codi que hi ha dins el bucle s'està executant tota l'estona, una vegada per *frame*. Un joc modern, acostuma a dibuixar la pantalla al menys 60 vegades per segon, per tant aquest codi s'estaria executant 60 vegades cada segon (diem que la frequència és de 60 herz, o cada 0.016 segons (1/60).

3. La funció `ClearBackground` fa que el fons de la finestra sigui de color negre. T'atreveixes a posar un altre color?

4. Sembla bastant evident què fa la funció `DrawRectangle`, oi? Però què volen dir els paràmetres? El primer (100) és la posició `x`, el segon, la `y`. Els tercers i quarts (10) son la mida (10 píxels) i el cinqué és el color. Prova de canviar la posició i la mida del rectangle. I el color?

5. Intenta endevinar quines coordenades fa servir el sistema. On és la posició x: 0 i y: 0? Quin és el limit de l'amplada? I de l'alçada?

6. Sabries com dibuixar un rectangle exactament al centre de la finestra?

7. Mira't la ["xuleta" de raylib](https://www.raylib.com/cheatsheet/cheatsheet.html), sabries com dibuixar una rodona en comptes d'un rectangle?
