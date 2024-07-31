var Serpiente = (función () {

const INICIAL_TAIL = 4;
var fixedTail = verdadero;

var interválido;

var tileCount = 10;
var tamaño de la cuadrícula = 400/tileCount;

Const_JUGADOR INICIAL = { x: Matemáticas. piso (tileCount / 2), y: Matemáticas. piso(tilecount / 2) };

Velocidad var = { x:0, y:0 };
jugador var = { x: JUGADOR_INICIAL. x, y: JUGADOR_ INICIAL. y };

paredes var = falso;

var fruta = { x:1, y:1 };

var trail = [];
var tail = COLA_INICIAL;

recompensa var = 0;
puntos var = 0;
var puntosMax = 0;

var ActionEnum = { 'ninguno':0, 'arriba':1, 'abajo':2, 'izquierda':3, 'derecha':4 };
Objeto. congelar (ActionEnum);
var últimaAcción = ActionEnum. Ninguno;

configuración de la función () {
    canv = document.getElementById('gc');
ctx = canv. getContexto('2d');

juego. restablecer();
  }

juego var = {

restablecer: función () {
CTX. FillStyle = 'gris';
CTX. fillRect(0, 0, canv. ancho, canv. altura);

cola = COLA_INICIAL;
puntos = 0;
velocidad. x = 0;
velocidad. y = 0;
Jugador. x = JUGADOR_INICIAL. x;
Jugador. y = JUGADOR_INICIAL. y;
// esto. Fruta Aleatoria();
recompensa = -1;

ÚltimaAcción = ActionEnum. Ninguno;

rastro = [];
Sendero. empuja({ x: jugador. x, y: jugador. y });
// for(var i=0; i<tail; i++) rastro. empuja({ x: jugador. x, y: jugador. y });
    },

Acción: {
arriba: función () {
Si (última acción! = ActionEnum. abajo){
velocidad. x = 0;
velocidad. y = -1;
        }
      },
abajo: función () {
Si (última acción! = ActionEnum. sus){
velocidad. x = 0;
velocidad. y = 1;
        }
      },
izquierda: función () {
Si (última acción! = ActionEnum. Correcto){
velocidad. x = -1;
velocidad. y = 0;
        }
      },
derecha: función () {
Si (última acción! = ActionEnum. izquierda){
velocidad. x = 1;
velocidad. y = 0;
        }
      }
    },

RandomFruit: función () {
si(paredes){
fruta. x = 1+Matemáticas. piso (Matemáticas. aleatorio() * (tileCount-2));
fruta. y = 1+Matemáticas. piso (Matemáticas. aleatorio() * (tileCount-2));
      }
Si no {
fruta. x = Matemáticas. piso (Matemáticas. aleatorio() * tileCount);
fruta. y = Matemáticas. piso (Matemáticas. aleatorio() * tileCount);
      }
    },

log: función () {
consola. tronco('===== =====>====+===');
consola. log('x:' + jugador. x + ', y:' + jugador. y);
consola. tronco('tail:' + cola + ', camino. longitud:' + sendero. longitud);
    },

bucle: función () {

recompensa = -0.1;

Función DontHitWall () {
si(jugador. Jugador x < 0). x = tileCount-1;
si(jugador. Jugador x >= tileCount). x = 0;
si(jugador. y < 0) jugador. y = baldosas de baldosas-1;
si(jugador. y >= tileCount) jugador. y = 0;
      }
función HitWall () {
si(jugador. x < 1) juego. restablecer();
si(jugador. Juego x > tileCount-2) restablecer();
si(jugador. y < 1) juego. restablecer();
si(jugador. y > tileCount-2) juego. restablecer();

CTX. FillStyle = 'gris';
CTX. fillRect(0,0, tamaño de la rejilla-1, canv. altura);
CTX. fillRect(0,0,canv. ancho, tamaño de la red-1);
CTX. FillRect (canv. ancho-Tamaño de rejilla +1,0, tamaño de rejilla, canv. altura);
CTX. fillRect(0, canv. altura-Tamaño de la rejilla +1, canv. ancho, tamaño de la cuadrícula);
      }

var detenido = velocidad. x == 0 && velocidad. y == 0;

Jugador. x += velocidad. x;
Jugador. y += velocidad. y;

si (velocidad. x == 0 && velocidad. y == -1) última acción = ActionEnum. arriba;
si (velocidad. x == 0 && velocidad. y == 1) última acción = ActionEnum. abajo;
si (velocidad. x == -1 && velocidad. y == 0) últimaAcción = ActionEnum. izquierda;
si (velocidad. x == 1 && velocidad. y == 0) últimaAcción = ActionEnum. correcto;

CTX. fillStyle = 'rgba(40,40,40,0.😎';
CTX. fillRect(0,0,canv. ancho,canv. altura);

if(muros) HitWall();
El otro no golpea el muro();

// juego. log();

si (! parado){
Sendero. empuja({x:player. x, y: jugador. y});
mientras (sendero. longitud > cola) sendero. turno();
      }

¡Si(! parado) {
CTX. fillStyle = 'rgba(200,200,200,0.2)';
CTX. Font = "pequeñas mayúsculas 14px Helvética";
CTX. fillText("(esc) reset", 24, 356);
CTX. fillText("(espacio) pausa", 24, 374);
      }

CTX. FillStyle = 'verde';
for(var i=0; i<trail. longitud-1; i++) {
CTX. fillRect(trail[i]. x * tamaño de cuadrícula +1, rastro[i]. y *Tamaño de cuadrícula +1, tamaño de cuadrícula-2, tamaño de la cuadrícula-2);

// consola. debug(i + ' => jugador:' + jugador. X, jugador. y + ', trail:' + trail[i]. x, rastro[i]. y);
si (! parado && rastro[i]. x == jugador. x && rastro[i]. y == jugador. y){
juego. restablecer();
        }
CTX. FillStyle = 'lima';
      }
CTX. fillRect(trail[trail. longitud-1]. x * tamaño de cuadrícula +1, rastro[sendero. longitud-1]. y *Tamaño de cuadrícula +1, tamaño de cuadrícula-2, tamaño de la cuadrícula-2);

si (jugador. x == fruta. Jugador x &&. y == fruta. y) {
¡Si(! Cola fija) cola++;
puntos++;
if(puntos > puntosMax) puntosMax = puntos;
recompensa = 1;
juego. Fruta Aleatoria();
// Asegúrate de que la nueva fruta no desove en la cola de serpiente
mientras((función () {
for(var i=0; i<trail. longitud; i++) {
si (trail[i]. x == fruta. x && rastro[i]. y == fruta. y) {
juego. Fruta Aleatoria();
volver verdadero;
            }
          }
devolver falso;
        })());
      }

CTX. FillStyle = 'rojo';
CTX. fillRect (fruta. x * rejilla+1, fruta. y *Tamaño de cuadrícula +1, tamaño de cuadrícula-2, tamaño de la cuadrícula-2);

si (detuvo) {
CTX. fillStyle = 'rgba(250,250,0.😎';
CTX. Font = "pequeñas gorras negrita 14px Helvética";
CTX. fillText ("presiona las CLAVES DE FLECHA para COMENZ ", 24, 374);
      }

CTX. FillStyle = 'blanco';
CTX. Font = "negrita pequeña-caps 16px Helvética";
CTX. fillText("puntos: " + puntos, 288, 40);
CTX. fillText("arriba: " + pointsMax, 292, 60);

recompensa de regreso;
    }
  }

Función keyPush (evt) {
cambio (evt. Código de clave) {
Caso 37: //izquierda
juego. Acción. izquierda();
Todo. Prevenir predeterminado();
descanso;

Caso 38: // arriba
juego. Acción. arriba();
Todo. Prevenir predeterminado();
descanso;

Caso 39: //derecho
juego. Acción. correcto();
Todo. Prevenir predeterminado();
descanso;

Caso 40: //abajo
juego. Acción. abajo();
Todo. Prevenir predeterminado();
descanso;

Caso 32: //espacio
Serpiente. pausa();
Todo. Prevenir predeterminado();
descanso;

Caso 27: //esc
juego. restablecer();
Todo. Prevenir predeterminado();
descanso;
    }
  }

volver {
inicio: función (fps = 15) {
ventana. descarga = configuración;
intervalID = setInterval (juego. bucle, 1000 / fps);
    },

bucle: juego. bucle,

restablecimiento: juego. restablecer,

parada: función () {
Intervalo claro (interválido);
    },

configuración: {
teclado: función (estado) {
si (estado) {
documento. AddEventListener('Clavado', keyPush);
} más {
documento. EliminarEscuchaEventos('Claydown', keyPush);
        }
      },
muro: función (estado) {
muros = estado;
      },
tileCount: función (tamaño) {
tileCount = tamaño;
Tamaño de la cuadrícula = 400 / baldosaCount;
      },
Cola fija: función (estado) {
Cola fija = estado;
      }
    },

Acción: función (acto) {
Cambio (actuar) {
Caso 'izquierda':
juego. Acción. izquierda();
descanso;

caso 'arriba':
juego. Acción. arriba();
descanso;

Caso 'derecho':
juego. Acción. correcto();
descanso;

Caso 'abajo':
juego. Acción. abajo();
descanso;
      }
    },

pausa: función () {
velocidad. x = 0;
velocidad. y = 0;
    },

clearTopScore: función () {
puntosMax = 0;
    },

datos: {
jugador: jugador,
fruta: fruta,
trail: función () {
rastro de regreso;
      }
    },

info: {
tileCount: tileCount
    }
  };

})();

Serpiente. inicio(8);
Serpiente. configuración. teclado (verdadero);
Serpiente. configuración. Cola fija (falso);
